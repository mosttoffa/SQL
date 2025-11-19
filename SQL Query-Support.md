## SQL Query 

## Create Table : 
Model/Entity name: MercCompanyWiseMercSettingEntity 
-----------------
Table: 
------
CREATE TABLE MERC_CompanyWiseMercSetting (
    ID NVARCHAR(50) PRIMARY KEY DEFAULT NEWID(),
	CompanyId NVARCHAR(50), 
	DdlKey NVARCHAR(50),
	CreatedBy NVARCHAR(50),
	CreatedDate NVARCHAR(50)

	);


-----Add another column SourceKey: 

ALTER TABLE MERC_CompanyWiseMercSetting
ADD SourceKey NVARCHAR(50);

-----------------------------------------------------
-- Truncate korle sob data delete hoye jabe and ID sob first theke hobe 
  Truncate Table MERC_CompanyWiseMercSetting
-----------------------------------------------------

## Update Query 

--	Update MERC_Query_FabricColourInfo set GmtColorId=NULL where Id in ('B7F63E15-C376-43BF-863E-9FDF0E3E350B','91B00084-D37D-469A-84BE-4E7EF59F8A85')

--------
--select * from MERC_Query_FabricColourInfo
--select * from HR_Region 
--select * from MERC_OrderBookingMaster where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA'

select * from MERC_BuyerInformation where ID='C93FAD59-BF89-45DA-997F-BD888DF63136'

select OrderNo from MERC_OrderBookingMaster where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA' and BuyerId='C93FAD59-BF89-45DA-997F-BD888DF63136'

--update MERC_OrderBookingMaster set OrderNo='KKCL/312/2025//RMFAR Inc.'where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA' and BuyerId='C93FAD59-BF89-45DA-997F-BD888DF63136'

------------------------------------------------------------

## A full Join Query of a Part
select A.FabricSerial,

A.Id, A.fabricColourInfoID, A.BPinfoID, A.ColourNameID, A.Remarks, A.CreatedBy, A.CreatedDate, A.UpdateBy, A.UpdateDate, A.fabficTypeId, A.fabficConstructionTypeID, A.CompositionID, A.gsmID, A.StyleOptionId, A.DyingInformation, A.DyingInformationText, 
A.FinishingInformation, A.FinishingInformationText, A.Printtypeid, A.BpGroup, A.FabLength, A.FabWidth, A.FabSortOrder, A.FabDesign, A.FabTypes, A.FabFileAttach, A.ColorCodeType, A.ColorNumber, A.FabConsumtion, A.FinishType, A.WidthInche, 
A.FabColorName, A.FabShadeId, A.OrderUnit, A.FabQtyKg, A.FabQtyYard, A.FabQtyMeter, A.FabProcessLoss, A.FabRate, A.FabTotalValue, A.FabUOM, A.FabCutOfWidth, A.FabComments, A.FabKnitRate, A.FabDyeingRate, A.TotalFabricQty, A.CuffLength, 
A.CuffHeight, A.FabricSource, A.FabYDRate, A.FabAOPRate, A.FabricGMTItemId, A.FabricNominitedSupplier, A.AOPPercentage, A.DyingPercentage, A.KnittingPercentage, A.AopRate, A.DiaFinish, A.FabConsumptionDzn, A.GMTItemName, A.FabGMTPerQty, 
A.FinishFabricQty, A.BreakdownSize, A.BreakdownConsumption, A.CollarStyleSize, A.CollarSize, A.CollarQty, A.CollarExcessQty, A.ConsumptionQty, A.CuffStyleSize, A.CuffSize, A.CuffQty, A.CuffExcessQty, A.CuffPercentage, A.CollarPercentage, 
A.FinishDias, A.DiaTypes, A.FabricConversionFlag, A.SizeWisePlanCutQuantity, A.SizeWiseFaricQty, A.GmtColorId, A.GraySize, A.GrayPlanCut, A.GrayConsumDzn, A.GrayFabQty, A.GrayFinDia, A.GrayFabDiaType, A.ChildDiaUOM, A.ChildGrayDiaUOM, 
A.ShedRangeId, A.SizeConsumptionInsideFraction, A.GraySizeConsumptionInsideFraction, A.FabItemId, A.FabStyleWiseRefId, A.UniqFabId

, (select Name from MERC_ColorName z where z.ID = A.FabShadeId) FabShadeName
,S.StyleOptionName,ST.StyleName,I.Name ItemName,YC.Name Composition, YT.Name Construction,
-- B.Name ColorName,S.QueryId,BD.Name BodyPartName,P.PrinttypeName, C.Name FabricTypeName,
CONCAT(ST.StyleName,' :: ',S.StyleOptionName,' :: ', BD.Name,' :: ',I.Name,' :: ',G.Name,' :: ',YC.Name) AS FabricName,
                   
CONCAT(BD.Name,':',I.Name,':',G.Name,':',YC.Name) AS FabricNameInfo,
CONCAT(YT.Name,':',YC.Name,':',G.Name) AS FabricConsumption,
CASE
WHEN FabricSource='1' THEN 'Production'
WHEN FabricSource='2' THEN 'Grey Purchase'
WHEN FabricSource='3' THEN 'Finish Purchase'
WHEN FabricSource='4' THEN 'Buyer Supplied'
ELSE 'Stock' END FabricSourceName
                      
,BD.Nature,G.Name GSM,S.AppOrderQty,FT.Name FabricNature
,S.PlanCutQty
,Sup.Name SupplierName
					 
,BD.ID BodyPartId
,A.FinishFabricQty FinFabricQty
,A.TotalFabricQty FabricQty
,IsNULL(YD.YarnConsum,0)YarnConsum
,IsNUll(ConsumptionQty,0)FabConsumptionQty
,Shd.ShadeRange
,Shd.ShadePercentage
                      
from 
MERC_Query_StyleOption S 
left join MERC_NewStyle I on S.ItemId=I.ID,
MERC_Query_StyleInfo ST,

MERC_BodyPart BD,MERC_Query_FabricColourInfo A 
left outer join MERC_ColorName B on A.GmtColorId=B.ID
left outer join MERC_FabricType C on A.fabficTypeId=C.ID
left outer join MERC_Printtype P on A.Printtypeid=P.ID
left join MERC_FabricGsm G on G.ID=A.gsmID
left join MERC_YarnType YT on YT.ID=A.fabficConstructionTypeID
left join MERC_YarnComposition YC on A.CompositionID=YC.ID
Left Join MERC_FabricType FT ON FT.Id=A.fabficTypeId
LEFT JOIN (Select FabricRefId,SUM(YarnConsum)YarnConsum from MERC_StripeMeasurementDetails GROUP BY FabricRefId) YD ON A.Id=YD.FabricRefId
LEFT JOIN MERC_ShadeRange Shd ON Shd.Id=A.ShedRangeId
Left Join MERC_Supplier Sup On Sup.Id=A.FabricNominitedSupplier
where 
S.Id=A.StyleOptionId and S.styleid=ST.id 
and BD.ID=A.BPinfoID  and S.QueryId ='ACF30D55-CF1B-481E-99B4-9C722102C593' order by FabricSerial

--Select * from MERC_ColorName
--Select GmtColorId from MERC_Query_FabricColourInfo where Id in ('B7F63E15-C376-43BF-863E-9FDF0E3E350B','91B00084-D37D-469A-84BE-4E7EF59F8A85')

--	Update MERC_Query_FabricColourInfo set GmtColorId=NULL where Id in ('B7F63E15-C376-43BF-863E-9FDF0E3E350B','91B00084-D37D-469A-84BE-4E7EF59F8A85')


--------
--select * from MERC_Query_FabricColourInfo
--select * from HR_Region 
--select * from MERC_OrderBookingMaster where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA'


select * from MERC_BuyerInformation where ID='C93FAD59-BF89-45DA-997F-BD888DF63136'

select OrderNo from MERC_OrderBookingMaster where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA' and BuyerId='C93FAD59-BF89-45DA-997F-BD888DF63136'

--RMFAR Inc.
--update MERC_OrderBookingMaster set OrderNo='KKCL/312/2025//RMFAR Inc.'where JobNo='312' and AreaId='617AC53E-C377-4CFF-A2DB-E55E561CA6BA' and BuyerId='C93FAD59-BF89-45DA-997F-BD888DF63136'
-- buying house:   RMFAR Inc.

--------------------------

	SELECT 
	A.Id,
	QM.QueryDate,
	-- Conditionl
	CASE 
	WHEN ISNULL(QM.SubmitStatus, 0) = 1 THEN 'Submitted'
	WHEN ISNULL(QM.SubmitStatus, 0) = 2 THEN 'Rejected'
	WHEN ISNULL(QM.SubmitStatus, 0) = 3 THEN 'Confirmed'
	ELSE 'Pending' 
	END AS SubmitStatusText,
	CASE
	WHEN FabricSource = '1' THEN 'Production'
	WHEN FabricSource = '2' THEN 'Grey Purchase'
	WHEN FabricSource = '3' THEN 'Finish Purchase'
	WHEN FabricSource = '4' THEN 'Buyer Supplied'
	ELSE 'Stock' 
	END AS FabricSourceName,
	A.FabricSource,
	FT.Name AS FabricNature,
	
	-- Init Value
	ISNULL(QM.SubmitStatus, 0) AS SubmitStatus,
	ISNULL(CM.ApStatus, 0) AS ConfirmStatus,
	CM.JobNo,
	S.StyleOptionName,
	ST.StyleName,
	(SELECT Name FROM MERC_ColorName z WHERE z.ID = A.FabShadeId) AS FabShadeName,
	I.Name AS ItemName,
	YC.Name AS Composition,
	YT.Name AS Construction,
	B.Name AS ColorName,
	A.ColourNameID ColorId,
	S.QueryId,
	BD.Name AS BodyPartName,
	BD.Id BodyPartId,
	P.PrinttypeName,
	C.Name AS FabricTypeName,
	-- Supplier Names Aggregation
	(
	SELECT STRING_AGG(CompanyName, ', ') 
	FROM MERC_Supplier 
	WHERE Id IN (
	SELECT TRY_CAST(s.value AS UNIQUEIDENTIFIER)
	FROM STRING_SPLIT(COALESCE(A.FabricNominitedSupplier, ''), ',') AS s
	WHERE TRY_CAST(s.value AS UNIQUEIDENTIFIER) IS NOT NULL
	)
	) AS SupplierName,

	S.AppOrderQty,
	A.FabricGMTItemId,
	GMT.Name AS GMTItemName,
	A.Printtypeid,
	P.PrinttypeName AS ColorType,
	A.FabTypes,
	A.FabDesign,
	FabCol.Name AS ColorName,
	G.Name AS GSM,
	A.DiaFinish,
	'Dia Type' AS DiaType, 
	A.FabUOM,
    
	ISNULL(A.FinishFabricQty, 0) AS FinishFabricQty,
	ISNULL(A.TotalFabricQty, 0) AS GrayQty,
	ISNULL(A.TotalFabricQty, 0) - (Isnull(FDet.PrevBookingQty,0)) BookingQty,
	(ISNULL(A.TotalFabricQty, 0) - Isnull(FDet.BookingQty,0)) AS Balance,
	Isnull(A.FabKnitRate,0)FabKnitRate,
	((Isnull(A.TotalFabricQty, 0) - isnull(FDet.PrevBookingQty,0)) * A.FabKnitRate) AS Amount,
	(Isnull(A.AOPPercentage,0) + Isnull(A.DyingPercentage,0) + isnull(A.KnittingPercentage,0)) as ProcessLoss
	,(Isnull(FDet.PrevBookingQty,0)+  Isnull(FDet.BookingQty,0)) PrevBookingQty
	,A.FabComments
	,S.Id StyleId
	,QM.BuyerId
	,A.FabricNominitedSupplier
	,QM.HouseId
	,QM.Id QueryId
	,Sup.CompanyName SupName
	,S.StylePoNo
	,A.FinishDias
	,A.DiaTypes
	,A.BreakdownSize
	,ST.StyleName
	,CM.JobNo
	,QM.QueryID
	FROM MERC_Query_FabricColourInfo A
	LEFT JOIN MERC_Query_StyleOption S ON S.Id = A.StyleOptionId
	LEFT JOIN MERC_NewStyle I ON S.ItemId = I.ID
	LEFT JOIN MERC_Query_StyleInfo ST ON S.StyleId = ST.Id
	LEFT JOIN MERC_OrderBookingMaster CM ON CM.QueryId = S.QueryId
	LEFT JOIN MERC_QuerySheetMaster QM ON QM.Id = S.QueryId
	LEFT JOIN MERC_BodyPart BD ON BD.ID = A.BPinfoID
	LEFT JOIN MERC_ColorName B ON A.ColourNameID = B.ID
	LEFT JOIN MERC_FabricType C ON A.fabficTypeId = C.ID
	LEFT JOIN MERC_Printtype P ON A.Printtypeid = P.ID
	LEFT JOIN MERC_FabricGsm G ON G.ID = A.gsmID
	LEFT JOIN MERC_YarnType YT ON YT.ID = A.fabficConstructionTypeID
	LEFT JOIN MERC_YarnComposition YC ON A.CompositionID = YC.ID
	LEFT JOIN MERC_FabricType FT ON FT.Id = A.fabficTypeId
	LEFT JOIN MERC_NewStyle GMT ON GMT.ID = A.FabricGMTItemId
	LEFT JOIN MERC_ColorName FabCol ON FabCol.Id = A.ColourNameID
	LEFT JOIN MERC_ColorType CType ON CType.Id = A.ColorCodeType
	Left Join (Select FA.Id FabricId, SUM(FD.PrevBookingQty)PrevBookingQty,SUM(FD.BookingQty)BookingQty
	from MERC_FabricBookingMaster M Left join MERC_FabricBookingDetails FD ON M.Id=FD.FbMId
	Left join MERC_Query_FabricColourInfo FA ON FA.Id=FD.FabricId
	Group By FA.Id) FDet
	ON FDet.FabricId=A.Id
	Left join MERC_Supplier Sup ON Sup.Id=A.FabricNominitedSupplier
	WHERE  1=1   and A.FabricSource='3' And CONVERT(DATETIME,QM.QueryDate,103)>=CONVERT(DATETIME,'01/09/2025',103) 
	And CONVERT(DATETIME,QM.QueryDate,103)<=CONVERT(DATETIME,'20/10/2025',103) and (ISNULL(A.TotalFabricQty, 0) - Isnull(FDet.BookingQty,0)) > 0 



------ this Query related question and answer: 


Why use ‘CASE’ here ?

eikhane CASE use kora hoyeche system er 1,2,3 esob number text value akare prokaser jonno Condition akare, then ELSE e value deowa hoyeche jno error show na kore 

Sub Query / Inner Select kore ki kora hoyeche eikhane ?

ekta SELECT query er vitore abr r 1ta SELECT query thakle setake Subquery / Inner query bole, eta usually main queryr data filter, calculation or comparison kore, Inner query ta age execute hoy then tar result jay 

‘- - Supplier Names Aggregation’ part e eikhane ki hoyeche ? eta ki uporer inner query er part ?

    eikhane COALESCE diye null value thakle empty string set kora hocche jno null thakle error na hoy,
    STRING_SPLIT comma separate korche,
    TRY_CAST diye protiti value k UNIQUEIDENTIFIER kora hocche , jodi kono value na thake tahole null return korbe error na, WHERE TRY_CAST(…) IS NOT NULL eta Invalid ID bad dicche
    STRING_AGG eta diye Supplier er j value/nam paowa gelo ta eksathe join korteche

Kivabe bujhbo kon Table ta eikhane Main Table hobe?

    Main table holo sei table jei table theke data fetch kora start hoy r baki table gulo sudhu Join hoye extra data dey
    Query always FROM er por j Table ta thake etai mainly Main table.

Base Table:

    Base table means Table ta Database e directly create kora and jar Data onno query theke na borong main stored record theke ase.

Join kno lagteche eikhane?

    Join lage ekadhik table theke related data eksathe anar jonno.

Kivabe bujhbo kon table kar sathe JOIN hobe?



------------------------------------------------------------------------------------------------------------------------------------












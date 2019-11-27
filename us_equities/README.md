Creating Codecs from MEMX SBE schema files
==========================================

Download or build the sbe-tool jar, it is needed to create the MEMO amd MEMOIR codecs.
Information about SBE, including downloading binaries, or building the binaries, and general use can
be found [here](https://github.com/real-logic/simple-binary-encoding/blob/master/README.md).

For the examples below it is assumed that the sbe.xsd and the MEMX SBE schema files are loded into a directory.

    $ pwd
    /sbe
    $ ls -la
    drwxr-xr-x  14 staff  staff    448 Nov 20 13:14 .
    drwxr-xr-x   5 staff  staff    160 Nov 20 10:52 ..
    -rw-r--r--   1 staff  staff  12521 Nov 20 12:07 MEMO.types.include.xml
    -rw-r--r--   1 staff  staff  45531 Nov 20 12:07 MEMO.v1.schema.xml
    -rw-r--r--   1 staff  staff   2264 Nov 20 12:07 MEMOIR-Depth-Snapshot.v1.schema.xml
    -rw-r--r--   1 staff  staff   8876 Nov 20 12:07 MEMOIR-Depth.v1.schema.xml
    -rw-r--r--   1 staff  staff   7763 Nov 20 12:07 MEMOIR-LastSale.v1.schema.xml
    -rw-r--r--   1 staff  staff   3281 Nov 20 12:07 MEMOIR-Symbology.v1.include.xml
    -rw-r--r--   1 staff  staff   2321 Nov 20 12:07 MEMOIR-Top-Snapshot.v1.schema.xml
    -rw-r--r--   1 staff  staff   5263 Nov 20 12:07 MEMOIR-Top.v1.schema.xml
    -rw-r--r--   1 staff  staff   3320 Nov 20 12:07 MEMOIR.common.include.xml
    drwxr-xr-x   4 staff  staff    128 Nov 20 12:06 lib
    -rw-r--r--   1 staff  staff  18341 Nov 20 13:12 sbe.xsd

Also, the sbe-tool (sbe-tool-LATEST-SNAPSHOT.jar) and the agrona jar (agrona-1.0.3.jar) that the sbe-tool jar
is dependent on have been downloaded or built into a lib directory.

    $ ls -la lib
    drwxr-xr-x   4 staff  staff     128 Nov 20 12:06 .
    drwxr-xr-x  14 staff  staff     448 Nov 20 13:14 ..
    -rw-r--r--   1 staff  staff  385871 Nov 20 10:53 agrona-1.0.3.jar
    -rw-r--r--   1 staff  staff  412970 Nov 20 10:53 sbe-tool-LATEST-SNAPSHOT.jar


In the examples below, the commands to run the sbe-tool to generate MEMX codecs are shown.
The resulting codec (java) files are also shown.
The codec files are stored in directories that include version information.
It is shown here as v{n} (where n will increment as new versions are released).
The directories for the resulting code will change as MEMX releases new versions.
Also the list of files generated for each schema will change as the message specs change over time.
The files listed here are representative of the files produced by the sbe-tool.


Generating MEMO Codecs
----------------------

The command:

    java -Dsbe.target.language=Java -Dsbe.output.dir=memoCodecs -Dsbe.errorLog=yes -Dsbe.java.generate.interfaces=true -Dsbe.validation.stop.on.error=true -Dsbe.xinclude.aware=true -Dsbe.validation.xsd=sbe.xsd -classpath lib/sbe-tool-LATEST-SNAPSHOT.jar:lib/* uk.co.real_logic.sbe.SbeTool MEMO.v1.schema.xml

Creates the MEMO codecs:

    $ pwd
    /sbe/memoCodecs/com/memx/us_equities/memo/v{n}
    $ ls -la
    drwxr-xr-x  71 staff  staff   2272 Nov 26 14:50 .
    drwxr-xr-x   3 staff  staff     96 Nov 26 14:50 ..
    -rw-r--r--   1 staff  staff   1661 Nov 26 14:50 CancelReasonCode.java
    -rw-r--r--   1 staff  staff   2470 Nov 26 14:50 CancelRejectReasonCode.java
    -rw-r--r--   1 staff  staff    933 Nov 26 14:50 CxlRejResponseToType.java
    -rw-r--r--   1 staff  staff   1099 Nov 26 14:50 DispMethodType.java
    -rw-r--r--   1 staff  staff   1552 Nov 26 14:50 ExchangeCode.java
    -rw-r--r--   1 staff  staff   4085 Nov 26 14:50 ExecInstTypeDecoder.java
    -rw-r--r--   1 staff  staff   3877 Nov 26 14:50 ExecInstTypeEncoder.java
    -rw-r--r--   1 staff  staff   1447 Nov 26 14:50 ExecType.java
    -rw-r--r--   1 staff  staff  29433 Nov 26 14:50 ExecutionReport_CanceledDecoder.java
    -rw-r--r--   1 staff  staff  19353 Nov 26 14:50 ExecutionReport_CanceledEncoder.java
    -rw-r--r--   1 staff  staff  69985 Nov 26 14:50 ExecutionReport_NewDecoder.java
    -rw-r--r--   1 staff  staff  41065 Nov 26 14:50 ExecutionReport_NewEncoder.java
    -rw-r--r--   1 staff  staff  29338 Nov 26 14:50 ExecutionReport_PendingCancelDecoder.java
    -rw-r--r--   1 staff  staff  20913 Nov 26 14:50 ExecutionReport_PendingCancelEncoder.java
    -rw-r--r--   1 staff  staff  66360 Nov 26 14:50 ExecutionReport_PendingNewDecoder.java
    -rw-r--r--   1 staff  staff  38233 Nov 26 14:50 ExecutionReport_PendingNewEncoder.java
    -rw-r--r--   1 staff  staff  38589 Nov 26 14:50 ExecutionReport_PendingReplaceDecoder.java
    -rw-r--r--   1 staff  staff  25592 Nov 26 14:50 ExecutionReport_PendingReplaceEncoder.java
    -rw-r--r--   1 staff  staff  28964 Nov 26 14:50 ExecutionReport_RejectedDecoder.java
    -rw-r--r--   1 staff  staff  20568 Nov 26 14:50 ExecutionReport_RejectedEncoder.java
    -rw-r--r--   1 staff  staff  46086 Nov 26 14:50 ExecutionReport_ReplacedDecoder.java
    -rw-r--r--   1 staff  staff  30479 Nov 26 14:50 ExecutionReport_ReplacedEncoder.java
    -rw-r--r--   1 staff  staff  25647 Nov 26 14:50 ExecutionReport_RestatementDecoder.java
    -rw-r--r--   1 staff  staff  16370 Nov 26 14:50 ExecutionReport_RestatementEncoder.java
    -rw-r--r--   1 staff  staff  25421 Nov 26 14:50 ExecutionReport_TradeBreakDecoder.java
    -rw-r--r--   1 staff  staff  17609 Nov 26 14:50 ExecutionReport_TradeBreakEncoder.java
    -rw-r--r--   1 staff  staff  29493 Nov 26 14:50 ExecutionReport_TradeCorrectionDecoder.java
    -rw-r--r--   1 staff  staff  19828 Nov 26 14:50 ExecutionReport_TradeCorrectionEncoder.java
    -rw-r--r--   1 staff  staff  31392 Nov 26 14:50 ExecutionReport_TradeDecoder.java
    -rw-r--r--   1 staff  staff  19004 Nov 26 14:50 ExecutionReport_TradeEncoder.java
    -rw-r--r--   1 staff  staff   1213 Nov 26 14:50 LastLiquidityIndType.java
    -rw-r--r--   1 staff  staff   8542 Nov 26 14:50 MassCancelDoneDecoder.java
    -rw-r--r--   1 staff  staff   6594 Nov 26 14:50 MassCancelDoneEncoder.java
    -rw-r--r--   1 staff  staff  22671 Nov 26 14:50 MassCancelRequestDecoder.java
    -rw-r--r--   1 staff  staff  16449 Nov 26 14:50 MassCancelRequestEncoder.java
    -rw-r--r--   1 staff  staff   6045 Nov 26 14:50 MessageHeaderDecoder.java
    -rw-r--r--   1 staff  staff   3718 Nov 26 14:50 MessageHeaderEncoder.java
    -rw-r--r--   1 staff  staff    676 Nov 26 14:50 MetaAttribute.java
    -rw-r--r--   1 staff  staff  53009 Nov 26 14:50 NewOrderSingleDecoder.java
    -rw-r--r--   1 staff  staff  31281 Nov 26 14:50 NewOrderSingleEncoder.java
    -rw-r--r--   1 staff  staff   1221 Nov 26 14:50 OrdStatusType.java
    -rw-r--r--   1 staff  staff    855 Nov 26 14:50 OrdType.java
    -rw-r--r--   1 staff  staff  12282 Nov 26 14:50 OrderCancelRejectDecoder.java
    -rw-r--r--   1 staff  staff   8302 Nov 26 14:50 OrderCancelRejectEncoder.java
    -rw-r--r--   1 staff  staff  29610 Nov 26 14:50 OrderCancelReplaceRequestDecoder.java
    -rw-r--r--   1 staff  staff  21083 Nov 26 14:50 OrderCancelReplaceRequestEncoder.java
    -rw-r--r--   1 staff  staff  19890 Nov 26 14:50 OrderCancelRequestDecoder.java
    -rw-r--r--   1 staff  staff  16163 Nov 26 14:50 OrderCancelRequestEncoder.java
    -rw-r--r--   1 staff  staff    938 Nov 26 14:50 OrderCapacityType.java
    -rw-r--r--   1 staff  staff   2155 Nov 26 14:50 OrderRejectReasonCode.java
    -rw-r--r--   1 staff  staff    830 Nov 26 14:50 PegType.java
    -rw-r--r--   1 staff  staff  24300 Nov 26 14:50 PendingMassCancelDecoder.java
    -rw-r--r--   1 staff  staff  17322 Nov 26 14:50 PendingMassCancelEncoder.java
    -rw-r--r--   1 staff  staff   3547 Nov 26 14:50 PriceTypeDecoder.java
    -rw-r--r--   1 staff  staff   2536 Nov 26 14:50 PriceTypeEncoder.java
    -rw-r--r--   1 staff  staff    901 Nov 26 14:50 RepriceType.java
    -rw-r--r--   1 staff  staff   1193 Nov 26 14:50 SelfTradePreventionType.java
    -rw-r--r--   1 staff  staff    930 Nov 26 14:50 SideType.java
    -rw-r--r--   1 staff  staff   1287 Nov 26 14:50 TimeInForceType.java
    -rw-r--r--   1 staff  staff    903 Nov 26 14:50 TradingSessionIDType.java
    -rw-r--r--   1 staff  staff   8451 Nov 26 14:50 TradingSessionStatusDecoder.java
    -rw-r--r--   1 staff  staff   5226 Nov 26 14:50 TradingSessionStatusEncoder.java
    -rw-r--r--   1 staff  staff   1060 Nov 26 14:50 TradingSessionStatusType.java
    -rw-r--r--   1 staff  staff   3425 Nov 26 14:50 UTCTimestampNanosDecoder.java
    -rw-r--r--   1 staff  staff   2562 Nov 26 14:50 UTCTimestampNanosEncoder.java

Generating MEMOIR Top Codecs
----------------------------

The command:

    java -Dsbe.target.language=Java -Dsbe.output.dir=memoirTopCodecs -Dsbe.errorLog=yes -Dsbe.java.generate.interfaces=true -Dsbe.validation.stop.on.error=true -Dsbe.xinclude.aware=true -Dsbe.validation.xsd=sbe.xsd -classpath lib/sbe-tool-LATEST-SNAPSHOT.jar:lib/* uk.co.real_logic.sbe.SbeTool MEMOIR-Top.v1.schema.xml

Creates the MEMOIR Top codecs:

    /sbe/memoirTopCodecs/com/memx/us_equities/memoir/top/v{n}
    $ ls -la
    drwxr-xr-x  32 staff  staff   1024 Nov 26 09:47 .
    drwxr-xr-x   3 staff  staff     96 Nov 26 09:47 ..
    -rw-r--r--   1 staff  staff  10910 Nov 26 09:47 BestBidDecoder.java
    -rw-r--r--   1 staff  staff   6756 Nov 26 09:47 BestBidEncoder.java
    -rw-r--r--   1 staff  staff  14933 Nov 26 09:47 BestBidOfferDecoder.java
    -rw-r--r--   1 staff  staff   8964 Nov 26 09:47 BestBidOfferEncoder.java
    -rw-r--r--   1 staff  staff  10876 Nov 26 09:47 BestBidShortDecoder.java
    -rw-r--r--   1 staff  staff   6747 Nov 26 09:47 BestBidShortEncoder.java
    -rw-r--r--   1 staff  staff  10972 Nov 26 09:47 BestOfferDecoder.java
    -rw-r--r--   1 staff  staff   6814 Nov 26 09:47 BestOfferEncoder.java
    -rw-r--r--   1 staff  staff  10938 Nov 26 09:47 BestOfferShortDecoder.java
    -rw-r--r--   1 staff  staff   6805 Nov 26 09:47 BestOfferShortEncoder.java
    -rw-r--r--   1 staff  staff    827 Nov 26 09:47 BooleanType.java
    -rw-r--r--   1 staff  staff   7073 Nov 26 09:47 ClearBookDecoder.java
    -rw-r--r--   1 staff  staff   4766 Nov 26 09:47 ClearBookEncoder.java
    -rw-r--r--   1 staff  staff  21747 Nov 26 09:47 InstrumentDirectoryDecoder.java
    -rw-r--r--   1 staff  staff  14739 Nov 26 09:47 InstrumentDirectoryEncoder.java
    -rw-r--r--   1 staff  staff   5999 Nov 26 09:47 MessageHeaderDecoder.java
    -rw-r--r--   1 staff  staff   3724 Nov 26 09:47 MessageHeaderEncoder.java
    -rw-r--r--   1 staff  staff    682 Nov 26 09:47 MetaAttribute.java
    -rw-r--r--   1 staff  staff   8855 Nov 26 09:47 RegShoRestrictionDecoder.java
    -rw-r--r--   1 staff  staff   5598 Nov 26 09:47 RegShoRestrictionEncoder.java
    -rw-r--r--   1 staff  staff  10800 Nov 26 09:47 SecurityTradingStatusDecoder.java
    -rw-r--r--   1 staff  staff   6567 Nov 26 09:47 SecurityTradingStatusEncoder.java
    -rw-r--r--   1 staff  staff    896 Nov 26 09:47 SecurityTradingStatusReasonType.java
    -rw-r--r--   1 staff  staff    972 Nov 26 09:47 SecurityTradingStatusType.java
    -rw-r--r--   1 staff  staff   7040 Nov 26 09:47 SnapshotCompleteDecoder.java
    -rw-r--r--   1 staff  staff   4798 Nov 26 09:47 SnapshotCompleteEncoder.java


Generating MEMOIR Depth Codecs
------------------------------

The command:

    java -Dsbe.target.language=Java -Dsbe.output.dir=memoirDepthCodecs -Dsbe.errorLog=yes -Dsbe.java.generate.interfaces=true -Dsbe.validation.stop.on.error=true -Dsbe.xinclude.aware=true -Dsbe.validation.xsd=sbe.xsd -classpath lib/sbe-tool-LATEST-SNAPSHOT.jar:lib/* uk.co.real_logic.sbe.SbeTool MEMOIR-Depth.v1.schema.xml

Creates the MEMOIR Depth codecs:

    $ pwd
    /sbe/memoirDepthCodecs/com/memx/us_equities/memoir/depth/v{n}
    $ ls -la
    drwxr-xr-x  39 staff  staff   1248 Nov 26 09:49 .
    drwxr-xr-x   3 staff  staff     96 Nov 26 09:49 ..
    -rw-r--r--   1 staff  staff    829 Nov 26 09:49 BooleanType.java
    -rw-r--r--   1 staff  staff  13033 Nov 26 09:49 BrokenTradeDecoder.java
    -rw-r--r--   1 staff  staff   7923 Nov 26 09:49 BrokenTradeEncoder.java
    -rw-r--r--   1 staff  staff   6969 Nov 26 09:49 ClearBookDecoder.java
    -rw-r--r--   1 staff  staff   4662 Nov 26 09:49 ClearBookEncoder.java
    -rw-r--r--   1 staff  staff  17153 Nov 26 09:49 CorrectedTradeDecoder.java
    -rw-r--r--   1 staff  staff  10182 Nov 26 09:49 CorrectedTradeEncoder.java
    -rw-r--r--   1 staff  staff  21749 Nov 26 09:49 InstrumentDirectoryDecoder.java
    -rw-r--r--   1 staff  staff  14741 Nov 26 09:49 InstrumentDirectoryEncoder.java
    -rw-r--r--   1 staff  staff   6001 Nov 26 09:49 MessageHeaderDecoder.java
    -rw-r--r--   1 staff  staff   3726 Nov 26 09:49 MessageHeaderEncoder.java
    -rw-r--r--   1 staff  staff    684 Nov 26 09:49 MetaAttribute.java
    -rw-r--r--   1 staff  staff  14554 Nov 26 09:49 OrderAddedDecoder.java
    -rw-r--r--   1 staff  staff   8572 Nov 26 09:49 OrderAddedEncoder.java
    -rw-r--r--   1 staff  staff   8967 Nov 26 09:49 OrderDeletedDecoder.java
    -rw-r--r--   1 staff  staff   5736 Nov 26 09:49 OrderDeletedEncoder.java
    -rw-r--r--   1 staff  staff  14890 Nov 26 09:49 OrderExecutedDecoder.java
    -rw-r--r--   1 staff  staff   8904 Nov 26 09:49 OrderExecutedEncoder.java
    -rw-r--r--   1 staff  staff  10973 Nov 26 09:49 OrderReducedDecoder.java
    -rw-r--r--   1 staff  staff   6811 Nov 26 09:49 OrderReducedEncoder.java
    -rw-r--r--   1 staff  staff  15053 Nov 26 09:49 OrderReplacedDecoder.java
    -rw-r--r--   1 staff  staff   9010 Nov 26 09:49 OrderReplacedEncoder.java
    -rw-r--r--   1 staff  staff   8857 Nov 26 09:49 RegShoRestrictionDecoder.java
    -rw-r--r--   1 staff  staff   5600 Nov 26 09:49 RegShoRestrictionEncoder.java
    -rw-r--r--   1 staff  staff  10802 Nov 26 09:49 SecurityTradingStatusDecoder.java
    -rw-r--r--   1 staff  staff   6569 Nov 26 09:49 SecurityTradingStatusEncoder.java
    -rw-r--r--   1 staff  staff    898 Nov 26 09:49 SecurityTradingStatusReasonType.java
    -rw-r--r--   1 staff  staff    974 Nov 26 09:49 SecurityTradingStatusType.java
    -rw-r--r--   1 staff  staff    775 Nov 26 09:49 SideType.java
    -rw-r--r--   1 staff  staff   7042 Nov 26 09:49 SnapshotCompleteDecoder.java
    -rw-r--r--   1 staff  staff   4800 Nov 26 09:49 SnapshotCompleteEncoder.java
    -rw-r--r--   1 staff  staff  12941 Nov 26 09:49 TradeDecoder.java
    -rw-r--r--   1 staff  staff   7822 Nov 26 09:49 TradeEncoder.java


Generating MEMOIR Last Sale Codecs
----------------------------------

The command:

    java -Dsbe.target.language=Java -Dsbe.output.dir=memoirLastSaleCodecs -Dsbe.errorLog=yes -Dsbe.java.generate.interfaces=true -Dsbe.validation.stop.on.error=true -Dsbe.xinclude.aware=true -Dsbe.validation.xsd=sbe.xsd -classpath lib/sbe-tool-LATEST-SNAPSHOT.jar:lib/* uk.co.real_logic.sbe.SbeTool MEMOIR-LastSale.v1.schema.xml

Creates the MEMOIR Last Sale codecs:

    $ pwd
    /sbe/memoirLastSaleCodecs/com/memx/us_equities/memoir/lastsale/v{n}
    $ ls -la
    drwxr-xr-x  28 staff  staff    896 Nov 26 09:50 .
    drwxr-xr-x   3 staff  staff     96 Nov 26 09:50 ..
    -rw-r--r--   1 staff  staff    832 Nov 26 09:50 BooleanType.java
    -rw-r--r--   1 staff  staff  21752 Nov 26 09:50 InstrumentDirectoryDecoder.java
    -rw-r--r--   1 staff  staff  14744 Nov 26 09:50 InstrumentDirectoryEncoder.java
    -rw-r--r--   1 staff  staff   6004 Nov 26 09:50 MessageHeaderDecoder.java
    -rw-r--r--   1 staff  staff   3729 Nov 26 09:50 MessageHeaderEncoder.java
    -rw-r--r--   1 staff  staff    687 Nov 26 09:50 MetaAttribute.java
    -rw-r--r--   1 staff  staff   8860 Nov 26 09:50 RegShoRestrictionDecoder.java
    -rw-r--r--   1 staff  staff   5603 Nov 26 09:50 RegShoRestrictionEncoder.java
    -rw-r--r--   1 staff  staff    825 Nov 26 09:50 SCExtendedHoursOrSoldType.java
    -rw-r--r--   1 staff  staff    974 Nov 26 09:50 SCSROTradeDetailType.java
    -rw-r--r--   1 staff  staff    812 Nov 26 09:50 SCSettlementType.java
    -rw-r--r--   1 staff  staff   1076 Nov 26 09:50 SCTradeThroughExemptionType.java
    -rw-r--r--   1 staff  staff  10805 Nov 26 09:50 SecurityTradingStatusDecoder.java
    -rw-r--r--   1 staff  staff   6572 Nov 26 09:50 SecurityTradingStatusEncoder.java
    -rw-r--r--   1 staff  staff    901 Nov 26 09:50 SecurityTradingStatusReasonType.java
    -rw-r--r--   1 staff  staff    977 Nov 26 09:50 SecurityTradingStatusType.java
    -rw-r--r--   1 staff  staff  19973 Nov 26 09:50 TradeCancelDecoder.java
    -rw-r--r--   1 staff  staff  11187 Nov 26 09:50 TradeCancelEncoder.java
    -rw-r--r--   1 staff  staff  32088 Nov 26 09:50 TradeCorrectDecoder.java
    -rw-r--r--   1 staff  staff  17403 Nov 26 09:50 TradeCorrectEncoder.java
    -rw-r--r--   1 staff  staff  19973 Nov 26 09:50 TradeReportDecoder.java
    -rw-r--r--   1 staff  staff  11187 Nov 26 09:50 TradeReportEncoder.java

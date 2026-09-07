let
    SeriesIds = {
        "JTS000000000000000QUR",
        "JTS000000000000000HIR",
        "JTS000000000000000JOR",
        "JTS000000000000000LDR"
    },

    RequestBody = "{
        ""seriesid"": [" & Text.Combine(List.Transform(SeriesIds, each """" & _ & """"), ",") & "],
        ""startyear"": ""2016"",
        ""endyear"": ""2026""
    }",

    Response = Web.Contents(
        "https://api.bls.gov/publicAPI/v2/timeseries/data/",
        [
            Headers = [#"Content-Type" = "application/json"],
            Content = Text.ToBinary(RequestBody)
        ]
    ),

    Json = Json.Document(Response),
    ResultsTable = Json[Results],
    SeriesList = ResultsTable[series],
    SeriesTable = Table.FromList(SeriesList, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    ExpandSeries = Table.ExpandRecordColumn(SeriesTable, "Column1", {"seriesID", "data"}, {"seriesID", "data"}),
    ExpandData = Table.ExpandListColumn(ExpandSeries, "data"),
    ExpandDataFields = Table.ExpandRecordColumn(ExpandData, "data", 
        {"year", "period", "periodName", "value"}, 
        {"Year", "Period", "PeriodName", "Value"}),
    #"Added custom" = Table.AddColumn(ExpandDataFields, "seriesID-", each if [seriesID] = "JTS000000000000000QUR" then "Quits Rate"
    else if [seriesID] = "JTS000000000000000HIR" then "Hires Rate"
    else if [seriesID] = "JTS000000000000000JOR" then "Job Openings Rate"
    else if [seriesID] = "JTS000000000000000LDR" then "Layoffs/Discharges Rate"
    else "Other"),
    #"Added custom 1" = Table.TransformColumnTypes(Table.AddColumn(#"Added custom", "Date", each #date(Number.FromText([Year]), Number.FromText(Text.Middle([Period], 1, 2)), 1)), {{"Date", type date}}),
    #"Renamed columns" = Table.RenameColumns(#"Added custom 1", {{"Date", "Date"}, {"seriesID-", "Metric"}}),
  #"Changed column type" = Table.TransformColumnTypes(#"Renamed columns", {{"Value", type number}, {"Year", Int64.Type}})
in
    #"Changed column type"

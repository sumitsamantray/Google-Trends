# Google-Trends Project [Link](https://app.powerbi.com/view?r=eyJrIjoiNzMzMmJjYjktOWNlNi00NmIzLWExNTYtYWUxMmZmMDAzM2M3IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

To use Google Trends API for fetching a dataset from https://serpapi.com/

Google Trends data on popular keywords across 69 countries. It emphasizes "Data Analyst" as the leading keyword with 55K searches, while "Data Engineer" is rising in popularity. Other notable keywords include "Web Developer," "Software Developer," and "Power BI Developer," with "Power BI Developer" accounting for the highest share at 35.5%. A performance graph tracks keyword trends over several days in October. The data is a snapshot of searches, indicating demand for various technical roles, with detailed analysis available for further tracking.

**Google Trends** regarding keyword performance over a certain period. It highlights the following:

- **Top keywords** such as "Data Analyst," which is associated with **55K searches**.
- **Rising keywords** like "Data Engineer."
- A detailed chart tracks keyword performance over several days (e.g., "Data Analyst," "Web Developer," "Software Developer," etc.), with "Power BI Developer" at 35.5%.

If you need deeper insights or visual improvements, let me know!


















After Pasting the codes into Power BI, replace your API Key in the code. If you don't know how to get the key, log in to https://serpapi.com/ and navigate to the account section, where you'll find it.

Keyword Limit: Maximum 5 Keywords can be passed.
  
  let
    // Define the API endpoint
    apiUrl = "https://serpapi.com/search.json",


// Define the parameters
queryParams = [ engine = "google_trends", q = "Data Analyst,The Developer,Jobs,India,Power BI" , data_type = "GEO_MAP", date = "today 5-y", tz="-330",api_key = "Paste your Key here"],

// Combine the endpoint and parameters
fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),

// Make the HTTP request
response = Web.Contents(fullUrl),

// Parse the JSON response
jsonResponse = Json.Document(response),

// Convert the response to a table
dataTable = Table.FromRecords({jsonResponse}),

// Extract the relevant data
comparedBreakdownByRegion = dataTable{0}[compared_breakdown_by_region]
in
    comparedBreakdownByRegion


This code is used to get data based on the date.

Keyword Limit : Maximum 5 Keywords can be passed


let
    // Define the base URL for the API call
    BaseUrl = "https://serpapi.com/search",

// Define the query parameters with engine, terms, data type, date, and time zone
QueryParams = [engine = "google_trends", q = "Data Analyst,The Developer,Jobs,India,Power BI",data_type = "TIMESERIES", date = "all", tz = "-330",    api_key = Key],

// Generate the full URL with query parameters
UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
    each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),

// Fetch data from the API
JsonResponse = Json.Document(Web.Contents(UrlWithParams)),

// Extract the "interest_over_time" part from the JSON response
InterestOverTime = JsonResponse[#"interest_over_time"]
in
    InterestOverTime

Code for past 7 days keywords performance data.

Keyword Limit : Maximum 5 Keywords can be passed.


let
    // Define the base URL for the API call
    BaseUrl = "https://serpapi.com/search",

// Define the query parameters with engine, terms, data type, date, and time zone
QueryParams = [engine="google_trends",q="Data Analyst,The Developer,Jobs,India,Power BI", data_type = "TIMESERIES",date = "now 7-d",tz = "-330",api_key = "Paste your key here"],

// Generate the full URL with query parameters
UrlWithParams = BaseUrl & "?" & Text.Combine(List.Transform(Record.FieldNames(QueryParams), 
    each _ & "=" & Uri.EscapeDataString(Record.Field(QueryParams, _))), "&"),

// Fetch data from the API
JsonResponse = Json.Document(Web.Contents(UrlWithParams)),

// Extract the "interest_over_time" part from the JSON response
InterestOverTime = JsonResponse[#"interest_over_time"]
in
    InterestOverTime


Code for related keywords where you'll get two categories of data: Rising Keywords and Top Keywords.

Keyword Limit : Maximum 1 Keywords can be passed


let
    // Define the API endpoint
    apiUrl = "https://serpapi.com/search.json",

// Define the parameters
queryParams = [engine = "google_trends",q = "The Developer",data_type = "RELATED_TOPICS",api_key = "Paste your Key"],

// Combine the endpoint and parameters to create the full URL
fullUrl = apiUrl & "?" & Uri.BuildQueryString(queryParams),

// Make the HTTP request and get the response
response = Web.Contents(fullUrl),

// Parse the JSON response
jsonResponse = Json.Document(response)
in
    jsonResponse


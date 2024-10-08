## DATA 512 -  Homework 1: Professionalism & Reproducibility

### Goal of the project
The goal of this project is to construct, analyze, and publish a time series dataset of monthly pageviews for a select set of Wikipedia articles related to rare diseases from July 1, 2015, to September 30, 2024. Data will be collected using the Wikimedia Analytics API, focusing on actual user pageview requests across desktop, mobile web, and mobile apps. The project emphasizes computational reproducibility by ensuring proper automation, origin tracking, and open reporting of results, with datasets stored as JSON files organized by article titles.

### License
This project is developed and distributed under the [MIT LICENSE](https://opensource.org/licenses/MIT), ensuring flexibility and openness for users and contributors. It allows anyone to use, modify, and distribute the code with minimal restrictions.
Under the MIT License, you are permitted to freely use the software for any purpose, but it comes with no warranty. The only requirement is that the original license and copyright notice must be included in any copies or substantial portions of the software.

### Data and Code Sources
 - **Wikimedia API** : https://wikimedia.org/api/rest_v1/
 
 Wikimedia projects are free, collaborative repositories of knowledge, written and maintained by volunteers around the world. Each project hosts a different type of content, such as encyclopedia articles on Wikipedia and dictionary entries on Wiktionary. The Analytics API gives you open access to data about Wikimedia projects, including page views, unique device, and more.

 Wikimedia API License and Terms of Use: https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use
 
 The Wikimedia API allows users to freely access and engage with its content. We can read and print articles or media at no cost, and are also free to share and reuse this content, provided it is done under open licenses hence making it appropriate for our usecase.

 **Page Views endpoint documentation:** https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/concepts/page-views.html

 <br>

- **Homework_1 template and cleaned data**: https://drive.google.com/drive/folders/1aR9pDJV2KWMSl_LR7BgMR5smwqqAHbWw

Work by: Prof. David MCDonald, Human Centered Design & Engineering (HCDE), University of Washington
<br>
https://www.hcde.washington.edu/mcdonald
<br>
dwmc@uw.edu

This folder contains the list or rare diseases cleaned and a sample template code which is used in our implementation as a starting point. The content is shared with the [CC-BY](https://creativecommons.org/licenses/by/4.0/) license. This allows us to copy, resdistribute, remix or transform the material but with appropriate credit and attribution.

### Data Files
`rare-disease_cleaned.AUG.2024.csv` : it consists of the list of rare disease titles, page id (unique identifier) and the Wikipedia link for each article. This cleaned data is used to query the Wikimedia /pageviews API to get the view count for each title.  This is a subset of the English Wikipedia that represents a large number of articles related to rare diseases. This list of pages was collected by using a database of rare diseases maintained by the [National Organization for Rare Diseases (NORD)](https://rarediseases.org) and matching them to Wikipedia articles that are either about a rare disease or have a section that mentions a rare disease

### Output Files
- **rare-disease_monthly_desktop_201507-202407.json** : Monthly desktop page traffic for all titles from 07-2015 till 07-2024

**Schema:**
```
{
    "<title_1>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ],
    "<title_2>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ]
    ...
}
```
<br>

- **rare-disease_monthly_mobile_201507-202407.json** : Monthly mobile page traffic for all titles including summation of data from 2 API calls i.e. mobile-web and mobile-app from 07-2015 till 07-2024

**Schema:**
```
{
    "<title_1>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ],
    "<title_2>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ]
    ...
}
```

<br>

- **rare-disease_monthly_cumulative_201507-202407.json** : Monthly traffic for all titles including summation of data from btoh desktop and mobile access types from 07-2015 till 07-2024

**Schema:**
```
{
    "<title_1>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ],
    "<title_2>": [
        {
            "project": "en.wikipedia",
            "granularity": "monthly",
            "timestamp": "2015070100",
            "agent": "user",
            "views": <view_count>
        },
        ...
    ]
    ...
}
```
<br><br>
To visualize the analysis of the rare diseases view counts across the timeframe, we create multiple graphs to understand the trend of specific pages under different analysis questions

- `max_min_avg.png` : contains time series for the articles that have the highest average page requests and the lowest average page requests for desktop access and mobile access over the entire time series

- `max_min_avg_logscale.png` : contains time series for the articles that have the highest average page requests and the lowest average page requests for desktop access and mobile access over the entire time series using the logarithmic scale for the views for better visualization of the titles with smaller values to prevent squashing of data points

- `top_10_desktop_mobile.png` : contains time series for the top 10 article pages by largest (peak) page views over the entire time series by access type

- `top_10_desktop_mobile_logscale.png` : contains time series for the top 10 article pages by largest (peak) page views over the entire time series by access type using the logarithmic scale for the views for better visualization of the titles with smaller values to prevent squashing of data points

- `fewest_months_10_desktop_mobile.png` : shows pages that have the fewest months of available data the 10 articles with the fewest months of data for desktop access and the 10 articles with the fewest months of data for mobile access

- `fewest_months_10_desktop_mobile_logscale.png` : shows pages that have the fewest months of available data the 10 articles with the fewest months of data for desktop access and the 10 articles with the fewest months of data for mobile access using the logarithmic scale for the views for better visualization of the titles with smaller values to prevent squashing of data points


### Known Issues
- The cleaned data present in the repository contains the title and links in the UTF-8 format. Hence, whle processing the fields we need to take care of the encoding format or to view the data using a text editor that is capable to viewing such encoded formats

- While making calls to the Wikimedia /pageviews API, the titles are supposed to have spaces replaced with "_" and be URL encoded for processing 

- There's no fixed limit on requests to the Wikimedia API, but your client may be blocked if you endanger the stability of the service. To stay within a safe request rate, wait for each request to finish before sending another request. Hence, it is recommended to have rate limits while accessing data from the public API. Refer `rare_disease_analysis.ipynb` for usage example
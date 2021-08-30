# Rotten Scripts Repository PR Analysis


## This document shows the statistial analysis of the repo "Rotten Scripts".
### Check out the repo *[here](https://github.com/HarshCasper/Rotten-Scripts)*.

# Check out the code [[here](https://github.com/Aditya-Komaravolu/PR-Analyzer/blob/main/PRScrapper.ipynb)].

## Step 1: Visit the target website

* ### First of all, the websites that we visit show interative data( or technically called as static data/display data).<b>

* ### Since the data is available and encoded with markup language, it can be retrieved and stored to make exploration analysis.<b>


* ### This itself is called Web Scraping,i.e, getting out all the necessary information from a website.<b>
![image](https://user-images.githubusercontent.com/64011471/131397259-3eb7ffd1-b2c8-4cc2-915e-1415758c4a84.png)

 
## Step 2: Locate the PR markup using Debugger 

* To enable the debugger, use `Fn + F12` key. 
* Trace out the location of the each PR container class manually.
* Here, as you can see the `class="Box-row Box-row--focus-gray p-0 mt-0 js-navigation-item js-issue-row"` is the required target class and the hieararchy is as follows:
    * `application-main`
      * `clearfix new-discussion-timeline container-xl px-3 px-md-4 px-lg-5`
        * `repository-content `
          * `js-check-all-container`
            * `....`
              * `....`
                * `Box-row Box-row--focus-gray p-0 mt-0 js-navigation-item js-issue-row navigation-focus`
 
  
![image](https://user-images.githubusercontent.com/64011471/131397987-63ad1aa6-8edc-4ad6-bcf5-51117a39cbaa.png)

* Once we locate the required class for the PR containers, then we can use a simple for loop to extract the `<a>` tag which contains the actual reference link to the PR location.
* Later we combine `href` along with `base_url: https://github.com/` to get the complete website link for each pull request.

## Step 3: PR status

  * GitHub has three states for any Pull Request namely, ***Open***, ***Closed*** and ***Merged***.
  * We have over 690+ PR's and hence is it very important to know the status of each of them.
  * Best way is to repeat step 2 and find the html tag which is associated with the Status data. Once you find out, we can use `BeautifulSoup` to fetch all the required tags with class as the condidtion, so that we get the status info.
  
## Step 4: Create a Pandas DataFrame
  * Now that we have `PR Links` and `Status` ready, it is time to combine them and store them together as a DataFrame (in simple terms, a table).
  ![image](https://user-images.githubusercontent.com/64011471/131401426-ee775ce1-3a4f-4473-b2bb-c0695cf2d318.png)
  
## Step 5: Fetch all the Contributors for each PR
  * We need the names of the contributors to better understand the diversity of the repo.
  * For that, we can again follow step 2 and get the required parameters.
  * Use `BeautifulSoup` to get the required tags containing the data of the contributors.
  * Later update the DataFrame by adding a new column to represent the Contributors.
  
  ![image](https://user-images.githubusercontent.com/64011471/131402166-78c4e372-e4da-40e7-91ba-a8a89107156f.png)

  
 ## Step 6: Distinct Contributors along with Count
  * We need to find out all the distinct contributors where every PR can involve more than one contributor.
  * For that we can write a nested for loop to append only if the string is different from all the strings which were added to the list in before iterations.To refer codebase, click [[here](https://github.com/Aditya-Komaravolu/PR-Analyzer/blob/main/PRScrapper.ipynb)].
  * Once done, we now have to compute the total number of contributions were done by each contributor in all the PR's. 
  * To calculate the count, define a for loop which tallies each and every contributor with the the actual column in the DataFrame.
  
 ## Step 7: Create a JSON File
  * WE can store the contributors and the count as key-value pairs in a dictionary.
  * Later use file pointer and json package to dump the dictionary as a json object.
 
  ## Step 8: Visualizing Data
  * Now that we have PR status and Total number of contributions by each contributor, we can plot them for better visualization of the entire repo.
  * I prefer `Bar Plots` for the current situation because we have categorical variables to represent and what else is better than a bar graph!  :)

  * ### PR status:
  
    ![image](https://user-images.githubusercontent.com/64011471/131405268-1ff889ba-81a5-46e5-b37e-d727df5bed62.png)
  
  * ### Top 5 Contributors:
  
    ![image](https://user-images.githubusercontent.com/64011471/131405338-d630d7fa-6ac9-4bc5-b98d-dd4f768de181.png)


  

# Tests_OpenBreweryAPI

# Intro
This is a simple test suite for the free API at https://www.openbrewerydb.org/ . API tests were created in Postman.
# Setup and run tests
1) Download and Install the latest Postman desktop client - https://www.postman.com/downloads/ 
2) Clone this repo, or copy the two .json files to your local machine.
3) Import the file 'OpenBreweryValidation.postman_collection.json' to Postman as a Collection - https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-postman-data
4) Launch the Collection Runner in Postman, by clicking the "Runner" button in the top-left.
5) In the Collection Runner window, select the Collection name "OpenBreweryValidation".
6) Next to "Data", click "Select File," and choose 'OpenBreweryTestData.json' from your file system.
7) (personal preference) In the checkboxes below, select "Save responses" and "Keep variable values".
8) Click the blue button "Run OpenBrewery..."

Test run should include 3 iterations of 4 requests each, and a total of 33 tests

# Test information
Each request is called with two happy-path tests (Iterations 1 and 2), and one negative test (Iteration 3)

## List Breweries 
https://api.openbrewerydb.org/breweries

Iteration 1  
- verifies filtering via the 'by_state' attribute, and 
- verifies the default number of results per page (20).

Iteration 2  
- verifies filtering via the 'by_state' attribute, 
- verifies 'per_page' attribute (results limited to 5, total for this state is 9), and
- verifies sorting (by city, descending order).

NOTE: There appears to be an error in either the API or the documentation for ascending/descending flag. https://www.openbrewerydb.org/documentation/01-listbreweries states that "+" produces descending order, but this seems to produce ascending order on the 'city' field (A to Z). This test has been left in a failure state.

## Get Brewery 
https://api.openbrewerydb.org/breweries/***

Iterations 1 and 2
- verify that the correct brewery entry is retrieved.

## Search Breweries 
https://api.openbrewerydb.org/breweries/search?query=***

Iterations 1 and 2
- verify that the expected number of results are retrieved.

## Autocomplete 
https://api.openbrewerydb.org/breweries/autocomplete?query=***

Iterations 1 and 2
- verify that the expected number of results are retrieved, and
- verify that each result contains the 'query' term in the name of the brewery itself.

NOTE: During manual testing I found that the autocomplete feature sometimes returns results when the city matches the query term (for example https://api.openbrewerydb.org/breweries/autocomplete?query=Alameda). These test cases do not include this kind of result, but this test could be expanded to allow results matching either field.

# Further development
I kept things relatively simple, but if this were expanded and maintained as a regression suite, goals would include:
1) Less reliance on static data. For example, when testing the 'sort' feature, each result could be compared alphabetically to the result after it, rather than comparing to a pre-set list. This will make the test stable over time. Since the DB was last updated 2 years ago, static data may be OK for now.
2) Refactor test data into multiple files. All test data - for query strings and results - is currently kept in a single file. Data items specific to different requests are separated by an extra return. Since .json files do not allow comments, this will be hard to read and interpret in a larger data set. 
3) Refactor collection/request structure. Iterating over each request the same number of times is somewhat limiting, as the 'List Breweries' request is more complex than others, and would warrant more unique tests. It could be separated into it's own collection with more iterations, or it could be copied into multiple requests that each focus on testing a different feature. (Query strings for this request also contain some blank attributes in each iteration, which is not ideal - adoption the latter approach would also solve this issue.)



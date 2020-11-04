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

1) List Breweries - https://api.openbrewerydb.org/breweries
Iteration 1  
- verifies filtering via the 'by_state' attribute, and 
- verifies the default number of results per page (20).
Iteration 2  
- verifies filtering via the 'by_state' attribute, 
- verifies 'per_page' attribute (results limited to 5, total for this state is 9), and
- verifies sorting (by city, descending order).
NOTE - there appears to be an error in either the API or the documentation for ascending/descending flag. https://www.openbrewerydb.org/documentation/01-listbreweries states that "+" produces descending order, but this seems to produce ascending order on the 'city' field (A to Z). This test has been left in a failure state.

2) 



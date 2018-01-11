# w3af-soapui-testsuite

## Setup

* Install [Docker](https://www.docker.com/) and [SoapUI](https://www.soapui.org/).
* Install and run the [w3af](http://w3af.org/) API Docker container from <https://hub.docker.com/r/andresriancho/w3af-api/>

      docker run -d -p 5000:5000 -p 9001:9001 andresriancho/w3af-api
  
* Verify the container setup by opening the url <http://localhost:5000> in a browser and checking the response:

      {
        "docs": "http://docs.w3af.org/en/latest/api/index.html"
      }
  
* Copy the SoapUI template project `w3af-pen-tests-soapui-project-tpl.xml` to `w3af-pen-tests-soapui-project.xml`, which will be customized for the actual tests.

## Running

* Start SoapUI and import the project file `w3af-pen-tests-soapui-project.xml`.
* Doubleclick the project node (*w3af pen tests*) to open the *project view* dialog and enter the following configuration values in the *properties* tab:
  
  * `target_urls` A comma separated list of urls to test (e.g. `http://localhost/site1, http://localhost/site2`)
  * `profile_file` The file name of the w3af profile to be used (default: `test_profile.pw3af`). The value will be interpreted relative to the project directory.

* Doubleclick the test suite node (*w3af pen tests* > *Run Tests*) to open the *test suite editor* and run the tests by clicking the green arrow.
* To obtain **information on the running tests** you can:
  * Doubleclick the *get status* test step to open it's editor. The JSON response tab is updated after each request.
  * Open the url <http://localhost:9001> in a browser to open the *Supervisor* dashboard. From there you can view the log files of the w3af process. 

## Results

After the tests are finished, a new result file will be created in the `results` directory (`results/project_name_YYYYMMdd_HHmmss.json`). To review the JSON formatted results in a readable way, open `results.html` in a browser and select the desired result file. 
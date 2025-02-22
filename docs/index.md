# Data Commons

[We're automating multi-country timelines for the UN Goals Section](https://datacommons.org/tools/statvar#s=dc%2Fs%2FUnitedNationsUn&d=dc%2Fd%2FUnitedNationsUn_SdgIndicatorsDatabase) within the [Statistical Variable Explorer](https://datacommons.org/tools/statvar) for our [Earthscape Chatbot UI fork](/earthscape/app/) - Filter by date and location on more than 10,000 statistical variables. Let's create a wrapper of Statistical Variable Explorer with [fewer hierarchy levels](https://datacommons.org/tools/statvar#s=dc%2Fs%2FUnitedNationsUn&d=dc%2Fd%2FUnitedNationsUn_SdgIndicatorsDatabase&sv=sdg%2FSI_POV_EMP1.AGE--Y15T24).

Here are our two active CoLabs for the Google Data Commons API:
1. [GDC-API-Caller CoLab](https://colab.research.google.com/drive/1phXc8z9IwmG9w83JTU4pXRv6XAV9a8BB?usp=sharing) - Directly calls the Google Data Commons API - Anna
2. [GDC-Parameters CoLab](https://colab.research.google.com/drive/1mZC2Pn4oKau9Sz1Q16_qnOK7Tai09uEo?usp=sharing) - Sends parameters to our caller, then works with fetched json data - Paul  

Copy the GDC-Parameters CoLab are rename it in your goal folder: GDC-Parameters-Air, etc.
Store the output in your goal's data subfolder. Let's figure out if we can call the CoLabs from Javascript.

## Goal Visualization

The [UN's seventeen 30-year goals](/data-pipeline/international/), plus four subsets of goal 9: Innovation.

1. [Good Paying Jobs](jobs)
2. [Healthy Food](food)
3. [Good Health](health)
4. [Quality Education](education)
5. [Gender Equality](women)
6. [Clean Water](water)
7. [Energy](energy)
8. [Healthy Economies](economy)
9. [Innovation](innovation)
10. [Inclusion](inclusion)
11. [Biodiversity](biodiversity)
12. [Conservation](conservation)
13. [Air and Climate](air)
14. [Aquatic](aquatic)
15. [Wildlife](wildlife)
16. [Peace and Justice](peace)
17. [Partnerships](partners)
18. [Balanced Budgets](balanced)
19. [Fast Reliable Transit](transit)
20. [High Speed Internet](internet)
21. [Expanding Livable Zones](space)
<br><br>

[The Python Data Loaders](https://docs.datacommons.org/tutorials/) are simpler than the Javascript ones. We'll instead send REST from Javascript to our Python Colabs to interact with the GDC API.

Finding DCID and property is one challenge in JavaScript, another is handling different JSON structures, which is not an issue when using the Python libraries, as can be seen in this [CoLab&nbsp;for&nbsp;Census&nbsp;Data](https://colab.research.google.com/github/datacommonsorg/api-python/blob/master/notebooks/analyzing_census_data.ipynb).

**Our Universal Filter Menus:**  
Age  
Income  
Gender  
Education  
<!--
The gender filter options could be:
- Male and Female (two lines)
- Female Only
- Male Only
- Combined (one line)
-->
<style>
table {
    display: block;
    width: 100%;
    width: max-content;
    max-width: 100%;
    overflow: auto;
    border: 1px solid #ccc;
}
table th {
	text-align: left;
	font-size: 16px;
	padding: 6px;
	border-bottom: 1px solid #ccc;
}
table td {
	padding: 6px;
}
</style>

## Commands

You'll use `yarn build` the most.  
`yarn dev` invokes https which requires installing a cert locally. (Ugh)

Instead, after you've run `python -m http.server 8887` in your webroot, view at:

[http://localhost:8887/data-commons/docs](http://localhost:8887/data-commons/docs/)  
[http://localhost:8887/data-commons/dist](http://localhost:8887/data-commons/dist/)


| Command           | Description                                              |
| ----------------- | -------------------------------------------------------- |
| `yarn install`    | Install or reinstall dependencies                        |
| `yarn dev`        | Start local preview server                             |
| `yarn build`      | Build your static site, generating `./dist`              |
| `yarn deploy`     | Deploy your project to Observable                        |
| `yarn clean`      | Clear the local data loader cache                        |
| `yarn observable` | Run commands like `observable help`                      |

<br>
When running "yarn build" the content of the docs folder is built into the dist folder.  The dist folder gets deleted each time the build is run. ("npm run build" is the equivalent cmd to use when the repo wasn't initiated with a yarn.lock file.) 

dist/ deployment is omitted within .ignore.
This allows us to avoid having merge conflicts.

index.html does not get built to dist. We add index.html to repos so we can insert localsite.js navigation. Sometimes we also put standard html in the index.html file, especially if it's not working in the build to dist.

Placing a span or div tag around the GDC-embeds in index.md allows them to work in the built dist output.

We can probably auto-build to dist when deploying to GitHub.
Try using the deploy.js sample Mike Bostock posted:
https://github.com/observablehq/framework/discussions/1030

[Our Setup Notes](../)

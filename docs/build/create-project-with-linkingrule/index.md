---
hide:
  - navigation
tags:
  - BeginnersTutorial
---

# Data Linking Tutorial

## Introduction

The eccenca DataIntegration platform is designed to support the process to "BUILD" a knowledge graph by integrating structured and unstructured data from multiple sources, including on-premises systems and cloud-based services.
The feature to BUILD include data mapping, transformation, and cleansing tools, as well as real-time data integration and governance support.

This beginner-level tutorial explains how to build a data integration project using linking rules.

The documentation consists of the following steps described in detail below:

1. Create a new project.
2. Upload files.
3. Create datasets
4. Create a linking task
5. Work with linking rules.

This tutorial shows how to connect two movie-related data sources and introduces some of Data-Integration’s fundamental functions. sources of information are LinkedMDB, the linked data version of the IMDb movie database, and DBpedia, the linked data version of Wikipedia. Both files contain a list of movies with their names, titles, release dates, and an internal ID for each movie. The task is to link the two datasets to find out which movie in DBpedia corresponds to which movie in LinkedMDB.

Sample CSV files: dbpedia.csv and linkedmdb.csv

[Links to dowload the files](**[https://drive.google.com/drive/folders/1LR-6d17LYTjsCr8ZOdJNVXI_QgkSfIIi](https://drive.google.com/drive/folders/1LR-6d17LYTjsCr8ZOdJNVXI_QgkSfIIi)**)

![image](sample.png)

The following material is used in this tutorial, you should download the files and have them at hand throughout the tutorial:

## Let's begin to create a project with the linking rules

### 1. **Create a new project.**

-   Once logged in to Corporate memory on the right side click on **create**

![image](create-project.png)

The screen gives an overview of the different projects created in your installation of Data Integration. It shows the item type on the left side like a project, workflow, dataset, transform, linking, and task.

-   Click on the **project** on the left side in the item type and double-click on the **project** in the centre.

![image](click-on-project.png)











- Type the project name as **Movie links** in the title field and click on **create.**

![image](type-movielinks.png)


**Step Result**: The project was created with the name "Movie links," which is displayed in the page top left corner.

![image](display-movielink.png)

### 2. **Upload the files**.

- Click on **add file** on the right side of the page.

![image](Add-file.png)

- Click on **drop files here** select the file and click on **open**.

![image](drop-files.png)

- Once the file is successfully uploaded click on **close.**
![image](uploaded.png)

- Repeat the same step to add the file select the next second file and upload it.

**Step Result**: The files are uploaded to the project and reflect on the right side as shown below.

![image](files-added.png)

### 3. **create datasets.**

- Click on **create.**

![image](click-on-create.png)

- Click on the **dataset** on the left side in the item type and double-click on the **CSV file** in the centre.

![image](click-on-project.png)

- Type the file name as **dbpedia** in **the** label field.

![image](dbpedia.png)

- Tick the option **select file from project** and select the file from the drop-down list of files available in the project.

![image](bdpedia-select-file.png)

- Click on **create**.

![image](bdpedia-create.png)

- Repeat the same step and add another file linkedmdb in the dataset.

- Create the empty dataset file for extracting both files' links as an output result. Click on the **dataset** on the left side of the item list and double-click on the **CSV** file.

![image](CSV.png)

- Type the label name **links.csv** in the label field.

![image](type-links.png)

- Tick the option **create empty file** and select the file name from the drop-down list as link.csv then click on create. 

![image](links.png)

**Step result**: Dataset for both the files dbpedia and linkedmdb has been created, and link.csv is created for the output result displayed in the page's center.

![image](dataset-created.png)
### 4.**Create a linking task.**

- Click on **create**.

![image](dataset-created.png)

- Click on **linking** on the left side in the item type and double-click on **linking** in the center.

![image](click-on-linking.png)

- Type the name as linking in the label field and select the source input data set as a dbpedia file.

![image](linking.png)

- Select the **type** field (it gives the default name) select the same and click on **create**.

![image](default-type.png)

- In the continuation to the same page go down, select the target input dataset as a linkedmdb file.

- Select the **type** field (it gives the default name) select the same and click on **create**.

![image](target-input.png)

- Select the **output dataset** as link.csv file.

![image](output.png)

- Click on create.

![image](linking-save.png)

**Step Result**: Linking task is created for the project. It shows the source path, target path, and operators (transform, comparison, and aggregation) options on the left side of the page.

![image](linking-result.png)

It shows the linking editor, linking execution, linking evaluation, and reference link in the centre of the page to create and evaluate the linking rules.

![image](linking-result.png)

On the right side of the page, it shows datasets, configuration linking, and configuration linking rules.

![image](linking-result.png)

### 5.**Work with linking rules : Assemble a linking rule with the linking editor.**

**Task**: To create a rule to say that movies from dbpedia and linkedmdb should be considered the same if their titles are identical.

- Click on the source path and drag the title on the canvas.

![image](source-path.png)

- Click on the target path and drag the title on the canvas.

![image](target-input.png)

**Step Result**: The titles from the source path and target are dragged on the canvas as shown below.

![image](source-target-path.png)

**Task**: Let's make this a little better and compare only the lowercase versions of the titles to get around issues with differences in the lower and upper case between the two datasets.

- Click on **transformation**, type the operator lowercase  in the search field and drag the same on the canvas twice.

![image](transformation1.png)

- Drag the little dot on the right side of the source path box onto the left dot of the transformation box(lower case) to connect the two with a line (you always must drag from the right side of one element to the left side of another to connect the two).

![image](source-conect-lower.png)

**Step Result**: The lines connected between the source path title and lowercase as shown below.

![image](source-conect-lower.png)

- Drag the little dot on the right side of the target path box onto the left dot of the transformation box(lower case) to connect the two with a line (you always must drag from the right side of one element to the left side of another to connect the two).

![image](target-lower.png)

**Step Result**: The lines connected between the target path title and lowercase as shown below.

![image](target-lower.png)

**Task**: To compare the movie title names of both the data dbpedia.csv and linkedmdb.csv.

- Click on **comparison** and type the equality in the search field and drag the string equality on the canvas.

![image](equality.png)

- Drag the little dot on the right side of both lowercase boxes onto the left dot of the string equality box to connect the two with a line (you always must drag from the right side of one element to the left side of another to connect the two).

![image](lower-equality.png)

**Step Result**: The lines are connected between both lowercase operators and string equality operators.

![image](lower-equality.png)

- Click on **save** on the right side of the page.

![image](save.png)

**Linking evaluation**: Now it is time to see your linking rule in action by running it on your datasets. So far, we have created a linking rule in which we changed the title names of both files in lowercase and compared the same. Now it’s time to generate the links by evaluating them.

- Click on the **linking evaluation**.

![image](linking-evaluation.png)

- Click on the **play button** to start the evaluation and generate the links.

![image](play.png)

**Step Result**: The links are generated as shown below. (It allows us to review the links and since Data Integration does not know which column to use as a unique identifier, it just uses the row number in the .csv file to identify each movie.

![image](play.png)

- Click on the down arrow button to expand all 

![image](expand.png)

**Step Result**: This allows you to see how the linking rule was performed for each link and even the movie name compared in both files.

![image](expand-result.png)

**Filter**: It has a filter feature that helps to find links by movie names. An example is shown below.

Let’s consider the movie name as shaft type shaft in the filter it shows the links with the shaft movie names links of both files.

![image](shaft.png)

Cross-checking in the dbpedia.csv and linkedmdb.csv data sheet.

![image](shaft-result.png)

The movie name is twice in both sheets, but the release dates differ. The shaft movie’s original release was in 1971 and the remake was in 2000. We have the tick option for the correct rule.

- Click on the linking execution then click on the play button to execute the links (It copies the links to our data file links.csv (which is our output file).

![image](linkexecution.png)

**Step Result**: The links are executed and copied to the output data file links.csv and which shows the count of links on the page.

**Thanks for learning**
**“Learning never exhausts the mind.”**








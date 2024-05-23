<div style="margin-right: 50px; margin-left: 30px;">

# Task 3: Create a metadata classifier
---

## Scope

In this exercise, we create a custom metadata classifier that finds any files with "draft-patent-filing" in the title. The rule should generate data finding if such a file is detected. 

* First, we define the classifier severity level as "Critical" to reflect the sensitive nature of the content. 
* Second, we rescan a bucket resource to see if our rule fires on any of its contents.
* Last, we verify our rule by reviewing the finding results. 

### Expected Outcomes

Once the rule is defined and the bucket is rescanned, we will see some findings for the metadata classifier. 

## Task 1. Create the metadata classifier rule

1. In the Wiz portal, navigate to **Policies > Data Classification Rules**, and then click the **Create New Data Classification Rule** button.

1. Under Classification Type, select **Metadata match**.

1. In the Name box, enter a name for this rule using the following format:
    <div style="margin-right: 150px;">
   
         <inject key="ODLUser"></inject>-dspmlab-meta
   
      </div>

1. (Optional) In the Description box, enter a description for the rule.
<br/>Use this field to provide context for other users. While unnecessary for this lab, best practice states the purpose of the rule and use cases that it is expected to address. For example, "Identify working patent documents that are not submitted or pending. The intention is to prevent accidental public exposure of such material prior to patent submission. Expected to scan Word, PDF, and text file titles with our required title string 'draft-patent-filing'."

1. From the Data Type dropdown, select **Other**.
<br/>As we are focused on proprietary information, this rule does not match known definitions, such as PHI or PII. As these types are used as filters in other pages, strive to keep them as accurate as possible.

     <p align="left">
       <img width="60%" alt="Metadata Classifier Rule Properties" style="border:black; border-width:1px; border-style:solid;" src="img/meta-data-class-descript.png"/>
     </p>

6. From the Severity dropdown box, select **Critical**.
<br/>Severity of the data classifier is only part of the formula used to designate the severity of a related data finding. Remember, it also considers the number of unique occurrences.

7. Under Matcher Logic in the Find text matching this Regex box, enter <code>.\*draft-patent-filing.\*</code>, which looks for the string 'draft-patent-filing' anywhere in the title of a file.
<br/>In this regular expression, the following is true:
   - <code>.*</code> matches any character (except for a newline) zero or more times, 
   - <code>draft-patent-filing</code> is the literal string you want to match, 
   - <code>.*</code> again matches any character zero or more times.
   This regular expression will match the string "draft-patent-filing" anywhere within the filename or file type.
   <br/>**Tip:** You can enter a few file name examples in the Test Text box, with the string appearing in various places within the filename, and    click Test Logic to make sure that it matches as you expect. It is best practice to validate the RegEx syntax before deploying it. When using https://regex101.com/, select the Golang flavor. If you are struggling with correct syntax, ChatGPT is adept at generating the text. Less specific is better. For example, the query 'I need a regular expression that matches for the string "draft-patent-filing" in any filename or file type' generates the expression used above. 


8. In the Minimum file size box, enter **1** and select **KB** in the Bytes drop down. 
<br/>**Tip:** Wiz recommends that you define a minimum file size to reduce the likelihood of false positives.
    <p align="left">
       <img width="60%" alt="Metadata Match Properties" style="border:black; border-width:1px; border-style:solid;" src="img/meta-data-match-criteria.png"/>
     </p>
<!-- ![Metadata Match Properties](img/meta-data-match-criteria.png) -->

9. Click **Create rule** to save the rule in the Wiz tenant.


# Save the data and attachment of an item from a SharePoint list to another SharePoint list

Need to save an item and attachment file from one SharePoint List to another SharePoint, based on a condition using Power Automate? check out this blog post.

In this blog post, I will show how you can use Power Automate to save an item and attachment from SharePoint list A to SharePoint list B and the attachment will be saved as a link.  



The Power Automate flow is in this Repository, you can easily download and change the connections and connection reference in the trigger and actions to your SharePoint site and list. 

**Note:** This step can be used where a SharePoint List are in the same SharePoint Site or where the SharePoint List are in different SharePoint Sites. 




### Use Case: Bank Customer Complaint Management

To illustrate the process, consider this example scenario:

Bank ABC operates a Customer Complaint Management System with various teams handling different categories of customer complaints.

They utilize the SharePoint list named 'Customer Complaints' and Customer Support Database. 

Whenever a new item is added to the Customer Complaint SharePoint list and 'Alert' is chosen from the 'Type of complaint' choice column, the system automatically stores the data and any attached files from the 'Customer Complaints' SharePoint list into the 'Customer Support Database' SharePoint list.
<br>

![figure1.png](/Images/figure1.png)
Figure 1: This shows the result of when an item is created in SharePoint list A, it automatically saves the item and attachment (as a link) in SharePoint list B. 

<br>
Disclaimer: This is not an actual bank, but a scenario I created.
<br>


### Trigger and Actions used in the flow 

-  When an item is created

-  Initialize variable

- Condition 
     - Get Attachments
     - Apply to each
       - Get attachment content 
       - Create file 
       - Create sharing link for a file or folder
       - Compose
       - Append to string variable
       - Create Item

<br>
In this context, the Customer Complaint SharePoint list will be referred to as SharePoint list A, and the Customer Support Database SharePoint list will be known as SharePoint list B. This distinction is intended to minimize confusion. 


#### Prerequisites
- Have a Power Automate license or access to use Power Automate.
- SharePoint Document Library (this will be used to save the attachment file gotten from SharePoint List A). 
- Have a Multiple line of text column in SharePoint list B, where the text format is rich text. This column will be used to save the link of the attachment saved in SharePoint list B. 

**Note:** The reason why we are using multiple line of text data type here instead of hyperlink data type column is because we are expecting more than one Attachment file and the date this blog post was written, hyperlink data type column does not support more than one hyperlink url. 
<br>

# Step by Step Process 



1. Go to <a href = "https://make.powerautomate.com/">Power Automate</a>

   ![figure2.png](Images/figure2.png)

   Figure 2: Power Automate Home Screen.

2. At the left-side of the screen, click on **Create**.

   ![figure3.png](Images/figure3.png)
   Figure 3: The Power Automate Home Screen displays a red arrow directing attention to 'Create' on the left side of the screen.
<br> 

   ![figure4.png](Images/figure4.png)
   Figure 4: Power Automate Create Screen.


3. At the middle of the screen, click on **Automated cloud flow**. Next, on Flow name add the name of the flow, here I will be using 

``` bash
 Populate Customer Support Database.
```

   On Choose your flow's trigger, select the trigger **When an item is created**. Next, click on the button **Create**, this is shown in figure 6.


   ![figure5.png](Images/figure5.png)
   Figure 5: A red arrow pointing to Automated cloud flow in the Power Automate Create screen.
 


   ![figure6.png](Images/figure6.png)
   Figure 6: Power Automate flow trigger: When an item is created. The arrow points where to write the flow's name, the trigger to choose, and where to click the button Create.


   ![figure7](Images/figure7.png)
   Figure 7: When an item is created trigger.

4. The trigger, 'When an item is created', select your SharePoint site and SharePoint list. Click on the drop-down icon next to **Site Address** to choose your SharePoint site, and then click on the drop-down icon next to **List Name** to select your SharePoint list.

   ![figure8](Images/figure8.png)
   Figure 8: A red arrow points to the selected SharePoint site and SharePoint list in the trigger when an item is created.

   **Note:** The flow is triggered when an item is created in the Customer Complaint SharePoint list (SharePoint List A).

5. Click on **+New step**, search and add the action **Initialize variable**. 

   ![figure9.png](/Images/figure9.png)
   Figure 9: A red rectangle showing the Initialize variable. 

6. In the **Name** field of the Initialize variable action add a word text, here I used Attachment. change the type of the initialize variable to String, this can be shown in figure 10. 

   ![figure10.png](/Images/figure10.png)
   Figure 10: The initialize variable

7. Click **+New step**, then search and add the **Condition** action.

   ![figure11.png](/Images/figure11.png)
   Figure 11: The Condition action.


8. On the left-side of the Condition action "Choose a value". Go to the Dynamic content, search and add the column you wish to base your condition on. For this example, I will select "Type of Complaint Value" a choice column (this is coming from the trigger when an item is created).

   Next, on Choose a Value on the right side, here I will write Alert as shown in figure 12. 

   <br>

   **Note:** We have options in the 'Type of Customer Complaint' choice column, but in this case, I want the flow to execute under the condition that whenever an item is created in the Customer Complaint SharePoint list and 'Alert' is selected as the type of complaint, the item and its attachment should be saved to the Customer Support Database.

   Next, modify 'Is equal to' to 'contains' as shown in figure 12.
<br>

   ![figure12.png](/Images/figure12.png)
   Figure 12: A red arrow points to the Choose a value at the right-side of the Condition action and another red arrows point to the Dynamic content "Type of Complaint Value". In the middle of the Condition action, a red arrow points to contains and at the right side of the Condition action a red arrow points to the word "Alert".


9. In the If yes of the Condition action, click on **Add an action**. Search and add the action **Get attachments**. Here, we will getting the attachment saved in SharePoint List A. In the Get attachments action, on Site Address select your SharePoint site and on List Name, select your SharePoint list name. 

   ![figure13.png](/Images/figure13.png)
   Figure13: Get attachment action; a red arrow showing where the SharePoint site and list has been selected.

10. The Get attachments action; on Id field go to the Dynamic content and search and select **ID** (this is coming from the trigger when an item is created), this is shown in figure 14. 


    ![figure14.png](/Images/figure14.png)
    Figure 14: A red arrow points to the Dynamics Content ID in the Id field of the Get attachments action.

11. Click on **Add an action**, search and add the action **Apply to each**.

    ![figure15.png](/Images/figure15.png)
    Figure 15:Apply to each action.


12. In the **Apply to each** action where we have **Select an output from previous steps**  go to your Dynamic content, search and select **body** (this is coming from the Get attachments action) this is shown in figure 16 and 17. 


   ![figure16.png](/Images/figure16.png)
   Figure 16:


   ![figure17.png](/Images/figure17.png)
   Figure 17: Apply to each action with the dynamic content body seleected. 



13. In the Apply to each action, click on **Add an action**, search and add the action **Get attachment content**. In the action, Get attachment content, select your SharePoint Site and SharePoint list (here we are getting the content of the attachment from SharePoint list A).


   ![figure18.png](/Images/figure18.png)
   Figure 18: The action, Get attachment content with the SharePoint site and list selected. 

14. In the Get attachment content action, on Id


   ![figure19.png](/Images/figure19.png)
   Figure 19: The Get attacment content action with the dynamic contents ID and Id selected. 

15. In the Apply to each action, click on **Add an action**, search and add the action **Create file** (this is SharePoint action). In the Site Address select your SharePoint site. This is will save the attachments gotten in SharePoint list A. 


   ![figure20.png](/Images/figure20.png)
   Figure 20: The action, Create file.

16. In the Create file action, on Folder path; click on the **folder icon** and then select your Document library. Here I will be selecting the folder Customers Complaint Database.


   ![figure21.png](/Images/figure21.png)
   Figure 21:

17. In the Create file action, on the **File Name** field go to the Dynamic content and select DisplayName (this is coming from the action, Get attachments) the result is shown in figure 22. In the **File Content** field, go to the Dynamic content and select Attachment Content (this is coming from the action, Get attachment content). 


   ![figure22.png](/Images/figure22.png)
   Figure 22:


18. Inside the Apply to each action, **click on Add an action** search and add the action **Create sharing link for a file or folder** (this is coming from the SharePoint action). Here we will be getting our SharePoint Document library. In the Site Address, select your SharePoint site, in the Library Name, select your SharePoint Document Library (For me this is Customers Complaint Database). 


   ![figure23.png](/Images/figure23.png)
   Figure 23:

19. In the Create sharing link for a file or folder, on Item Id; go to the Dynamic content, search and add the dynamic content **ItemId**. On **Link Type** click on the drop-down and select View and edit. On **Link Scope** click on the drop-down icon and select **People in your organization**.

   ![figure24.png](/Images/figure24.png)
   Figure 24: 


20. Inside the Apply to each action, click on Add an action, search and add the action **Compose**. 


   ![figure25.png](/Images/figure25.png)
   Figure 25:

21. In the Compose action, add the copy and paste the HTML hyperlink below. 

```html
<a href ="Link">Name</a><br>
```
   ![figure26.png](/Images/figure26.png)
   Figure 26:


22. In the Compose action, where we have Link remove it and go to Dynamic content, search and add the dynamic content **Sharing Link** (this is coming from the action create sharing link for a file or folder). Next, in the HTML hyperlink, remove the Name text and add the dynamic content **Display Name** (this is coming from the action, Get attachments).

   ![figure27.png](/Images/figure27.png)
   Figure 27: 


23. After the Compose action, inside the Apply to each action click on Add an action, search and add the action **Append to string variable**. Append to string variable; In the Name field, click on the drop-down icon and select Attachment (this is a variable coming from Initialize variable). In Value, go to dynamic content and select the output coming the **Compose** action, this is shown in figure 28. 


   ![figure28.png](/Images/figure28.png)
   Figure 28:


24. Here, we will be storing the items retrieved from the Customer Complaint SharePoint list (SharePoint list A) into the Customer Support Database (SharePoint list B). In the Apply to each action, click on **Add an action**, search and add the action **Create item** (this is an action from SharePoint). 

   ![figure29.png](/Images/figure29.png)
   Figure 29: The Create item action with the SharePoint site and list selected. 



25. Now, let's add the data from the columns we wish to save from the Customer Complaint (SharePoint list A) to the Customer Support Database (SharePoint list B). Create item action; in the 'AccountNumber' field, from the dynamic content, search and select the 'AccountNumber' dynamic content originating from the trigger when an item is created.

   ![figure30.png](/Images/figure30.png)
   Figure 30:

26. Create Item action; In the Attachment link field go to the dynamic content and select the variable "Attachments" this is coming from the Append to string variable. 
    ![figure31.png](/Images/figure31.png)
    Figure 31: 

<br>

   ![figure32.png](/Images/figure32.png)
    FIgure 32:
  
<br>
     Now go ahead and save the flow and also test the flow. 

![figure33.png](/Images/figure33.png)
Figure 33: The Apply to each action with all the actions added inside it. 

   
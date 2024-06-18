# Save-the-data-and-attachment-of-an-item-from-a-SharePoint-list-to-another-SharePoint-list
<p> My name is <a href ="https://www.linkedin.com/in/rachelirabor/">Rachel Irabor</a>, and I’m an MVP for Microsoft Business Application, Power Platform and Dynamics 365 CRM developer and trainer. I love to document what I have learned or encountered. <p></p>
<br>

Subscribe for the latest <a href ="https://www.linkedin.com/newsletters/ms-business-applications-7056225625308553216/">newsletters</a> and <a href = https://rachelirabor8.medium.com>articles</a> from my Medium and LinkedIn accounts.



<p>If you're working on a solution to save an attachment file from one SharePoint List to another, or need to save the data and attachment of an item from a SharePoint list to a different SharePoint list, check out this blog post </p>.

<br>

This can work when an item is created in SharePoint list A and you want the data and attachment created to be saved in another SharePoint list when a condition is met. 



<h2> <b>Use Case: Bank Customer Complaint Management</b></h2>
<p>To illustrate the process, consider this example scenario:

Bank ABC operates a Customer Complaint Management System with various teams handling different categories of customer complaints.

They utilize a SharePoint list named 'Customer Complaints'. Whenever a new item is added to this list and the 'ATM card' is chosen from the 'Type of complaint' choice column, the system automatically stores the data and any attached files from the 'Customer Complaints' SharePoint list into the 'Customer Support Database' SharePoint list.



Disclaimer: This is not an actual bank, but a scenario I created.
</p>


<h3> <b>Actions to add to your flow to make it possible to save an attachment from SharePoint list A to SharePoint list B</b></h3>

1. Get Attachment action

2. Get Attachment Content Action

3. Add Attachment Action

<br>
<p> In this context, the Customer Complaint will be referred to as SharePoint list A, and the Customer Support Database will be known as SharePoint list B. This distinction is intended to minimize confusion. </p>


<p><b>Prerequisites</p></b>
<p> Have a Power Automate license/ Developer Account or access to use Power Automate.</p>

<br>

<h2><strong>Step by Step Process </strong></h2>
1. Go to <a href = "https://make.powerautomate.com/">Power Automate</a>

![figure2.png](images/figure2.png)

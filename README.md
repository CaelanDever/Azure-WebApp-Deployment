# Azure WebApp Deployment

<img width="945" alt="6q" src="https://github.com/user-attachments/assets/496b842c-e401-4353-aa71-24160b7eb173" />

---

This README will walk you through creating and deploying a pretty cool web app on Azure. Along the way, you’ll learn essential Azure concepts such as Resource Groups, App Service Plans, and Web Apps.

# Key Concepts Displayed

1. Azure Resource Groups

2. App Service Plan creation and tiers

3. Deploying to Azure Web Apps

4. Navigating the Azure Portal and Kudu (Advanced Tools)
---

# Create a Resource Group

In the left-hand menu (or from the main dashboard), click Resource groups.

Click + Create or + Add (the exact button may vary slightly).

You’ll be prompted to fill in the following:

Subscription: Choose your Azure subscription.

Resource group: Enter a unique name (e.g., rg-beginner-project).

Region: Select a location close to you (e.g., East US, West Europe, etc.).

<img width="565" alt="1q" src="https://github.com/user-attachments/assets/c780d814-b02d-4fc6-a909-c6562397ddf4" />

Click Review + create and then Create.

<img width="310" alt="1qq" src="https://github.com/user-attachments/assets/af85ceaf-5405-467b-ac32-3208ca323d27" />

Reasoning:

A Resource Group is a logical container for Azure resources. By grouping your resources, you can manage and track them more easily (especially useful for cost management and organization).
---

# Create an App Service Plan

In the Azure Portal’s top search bar, type “App Service plans” and select the result.

Click + Create.

On the “Basics” tab, fill in the details:

Subscription: Your Azure subscription.

Resource Group: Select the resource group you created (e.g., rg-beginner-project).

Name: Enter a name (e.g., plan-beginner).

Region: Use the same location you chose for the resource group.

Pricing Plan: For a beginner project, you can choose the Free or Shared tier if available, or a low-cost tier like Basic (B1).

Click Review + create and then Create.

<img width="444" alt="2q" src="https://github.com/user-attachments/assets/572ce21f-c950-4bc3-ab7f-27158eb0bc65" />

Reasoning:

An App Service Plan defines the underlying compute resources for your web app. It controls how much you pay for compute, which region the resources run in, and what features are available.

---

# Create a Web App

From the Azure Portal dashboard (or left menu), click + Create a resource.

Search for Web App in the Marketplace and select Web App.

Click Create.

On the Basics tab:

Subscription: Select your subscription.

Resource Group: Choose the same resource group you created (rg-beginner-project).

Name: Enter a unique name (e.g., beginner-webapp-123). This name must be globally unique because it forms part of the web app’s URL: https://<app_name>.azurewebsites.net.

Publish: Select Code (since we’re just deploying static HTML).

Runtime stack: If you’re only deploying static HTML, you can pick something minimal or even select .NET, Node, or any stack that’s available.

Operating System: Choose Windows (for simplicity).

Region: Same region you used before.

App Service Plan: Click Change Plan, select the App Service Plan you just created.

SKU and size: Confirm the pricing tier you chose.

Click Review + create, and then Create.

<img width="469" alt="3q" src="https://github.com/user-attachments/assets/5c4bfa0c-8ce6-44f2-ad62-05b60e428159" />

Reasoning:

A Web App is the resource that hosts your web application code. Attaching it to your App Service Plan allows it to use the allocated compute resources.

---

# Deploy Your "Cool” Page

You have multiple ways to deploy your web content to Azure (e.g., using FTP, Visual Studio Code, or Azure CLI). For simplicity, we’ll use the Azure Portal’s built-in editor (called the App Service Editor) or Upload feature:

Go to your newly created Web App from the Azure Portal (search for it by name or find it in the Resource Group).

In the left-hand menu, under Development Tools, click App Service Editor (sometimes labeled Advanced Tools (Kudu) or VS Code in Web).

Click Go or Open.

You’ll open an editor environment in a new tab.

Navigate to site/wwwroot.

Create a new file called index.html (if it doesn’t exist).

<img width="742" alt="4q" src="https://github.com/user-attachments/assets/839b1d7e-7cdc-4700-925d-9ce10df5fbe0" />


Paste the “cool” HTML you prepared:

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Cool HTML Webpage</title>
  <style>
    /* Body Reset and Base Styles */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      font-family: "Helvetica Neue", Arial, sans-serif;
      color: #fff;
      background: linear-gradient(135deg, #1f4037 0%, #99f2c8 100%);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
      overflow-x: hidden;
    }

    /* Animated Background Circles */
    .circle {
      position: absolute;
      border-radius: 50%;
      opacity: 0.5;
      animation: float 10s infinite ease-in-out alternate;
    }
    .circle:nth-child(1) {
      width: 200px;
      height: 200px;
      top: 10%;
      left: 5%;
      background: rgba(255, 255, 255, 0.2);
    }
    .circle:nth-child(2) {
      width: 300px;
      height: 300px;
      top: 50%;
      right: 10%;
      background: rgba(255, 255, 255, 0.2);
      animation-delay: 2s;
    }
    .circle:nth-child(3) {
      width: 150px;
      height: 150px;
      top: 80%;
      left: 30%;
      background: rgba(255, 255, 255, 0.2);
      animation-delay: 4s;
    }

    @keyframes float {
      0% {
        transform: translateY(0px);
      }
      100% {
        transform: translateY(-40px);
      }
    }

    /* Main Container */
    .container {
      position: relative; /* ensures the circles don’t overlap container content */
      z-index: 1;         /* places container in front of the circles */
      text-align: center;
      max-width: 800px;
    }

    /* Title and Headline */
    h1 {
      font-size: 3rem;
      margin-bottom: 20px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    p.tagline {
      font-size: 1.2rem;
      margin-bottom: 40px;
      line-height: 1.5;
      color: #eaf6f5;
    }

    /* Button Styles */
    .cool-btn {
      display: inline-block;
      padding: 15px 30px;
      margin: 5px;
      font-size: 1rem;
      color: #1f4037;
      background-color: #fff;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .cool-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 15px rgba(0,0,0,0.3);
    }

    /* Card Section */
    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      grid-gap: 20px;
      margin-top: 40px;
    }
    .card {
      background-color: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(5px);
      padding: 20px;
      border-radius: 10px;
      transition: transform 0.3s;
    }
    .card:hover {
      transform: translateY(-5px);
    }
    .card h3 {
      margin-bottom: 10px;
      font-size: 1.4rem;
    }
    .card p {
      font-size: 1rem;
      line-height: 1.4;
      color: #d4f3ee;
    }

    /* Responsiveness */
    @media (max-width: 600px) {
      h1 {
        font-size: 2rem;
      }
      .cool-btn {
        width: 100%;
        margin-bottom: 10px;
      }
    }
  </style>
</head>
<body>
  <!-- Floating Circles for Decoration -->
  <div class="circle"></div>
  <div class="circle"></div>
  <div class="circle"></div>

  <div class="container">
    <h1>Welcome to My Cool Page</h1>
    <p class="tagline">
      This is a simple example of how to build a modern, fun webpage using HTML and CSS. 
      Feel free to tweak the styles, colors, and content to make it your own!
    </p>

    <button class="cool-btn" onclick="alert('You clicked the cool button!')">Click Me</button>
    <button class="cool-btn">Another Button</button>

    <div class="cards">
      <div class="card">
        <h3>Card One</h3>
        <p>
          Use this space to highlight an important piece of information. 
          Card layouts can make content more approachable.
        </p>
      </div>
      <div class="card">
        <h3>Card Two</h3>
        <p>
          Cards are modular, so you can easily add or remove them as needed. 
          Customize the size and style to match your personal taste.
        </p>
      </div>
      <div class="card">
        <h3>Card Three</h3>
        <p>
          Experiment with different animations, hover effects, and background 
          patterns to create a truly unique look.
        </p>
      </div>
    </div>
  </div>
</body>
</html>


<img width="711" alt="5q" src="https://github.com/user-attachments/assets/6771918d-5d88-42e5-927e-0e18b7b1722d" />

Save the file.

Reasoning:

The App Service Editor is convenient for quick edits or uploading single files directly to your web app’s root folder.

---

# Test Your Deployed Website

Navigate back to your Web App’s Overview page in the Azure Portal.

Locate the URL field (e.g., https://beginner-webapp-123.azurewebsites.net).

Click or open that URL in your browser.

You should see the “Welcome to My Cool Page” message you entered in index.html.



https://github.com/user-attachments/assets/acf4bf86-7ed8-40c6-a549-bbb5f44763b7



Reasoning:

Verifying deployment ensures everything is running correctly. The URL is publicly accessible, so anyone with the link can see your page unless you enable further authentication or restrictions.
---

# Summary and Next Steps

What You Did

Created a Resource Group: A container to hold your Azure resources.

Created an App Service Plan: Defined how you pay for compute resources.

Created a Web App: Hosted your web application code.

Deployed a Static Site: Learned how to quickly push content to Azure.

Verified Deployment: Confirmed your site is live.
---

What You Learned

Azure Portal Navigation: You explored the main tools and how to create/manage resources in Azure.

Resource Groups: Helpful for organizing and managing costs.

App Service Basics: The difference between an App Service Plan (the “container” for resources) and a Web App (the “deployment target” for your code).
---

Possible Next Steps

Deploy a more complex app (e.g., Node.js, Python, .NET, or Java).

Explore Continuous Deployment using GitHub or Azure DevOps.

Set up Custom Domains and HTTPS for your Web App.

Add Application Insights to track performance and errors.

Experiment with Azure Functions to create serverless backends.




![](./media/image1.png)

**Lab 1 - Designing APIs using Swagger**

**Overview**

![](./media/image2.png)

An API is an interface between the provider of some backend system(s)
who wants to expose a set of services and the consumers of those
services who want to do something with them. Adherence to a “contract”
or a clear understanding of what the requests and responses should look
like, makes life easier for all participants. In order to clearly
communicate the terms of that contract, the industry has created a few
formats for describing an API, the most popular of which is called
[*Swagger*](http://swagger.io/).

![](./media/image3.png)

By designing your API in Swagger, you allow the API developer and the
API consumer to both do their jobs and meet successfully in the middle
without unpleasant surprises.

![](./media/image4.png)

Apigee is a key contributing member of and has partnered with a number
of other companies to help drive the Swagger spec and contribute open
source software to the community.

This is a partial list of the tools that Apigee has created,
open-sourced, or contributed to related to API-first design, Swagger, or
API deployment:

-   [*http://apistudio.io*](http://apistudio.io/) - In-browser Swagger
    IDE including live documentation, code generation, mocking, and
    cloud hosting.

-   [*https://github.com/apigee-127/a127-documentation/wiki*](https://github.com/apigee-127/a127-documentation/wiki) -
    A toolkit for modeling and building rich, enterprise-class APIs in
    Node.js on your laptop.

-   [*http://editor.swagger.io*](http://editor.swagger.io) - This editor
    is the basis for the ones used in the above two projects, but it
    also includes code generators for a number of other languages.

**Objectives**

In this lab, we will describe an API contract in Swagger and invoke the
API in the cloud. We will also see how an API contract in Swagger can be
used to create an API proxy in Apigee Edge.

**Prerequisites**

Your Apigee Edge organization name, user name, and the password. Ask
your Instructor for organization and application details.

**Estimated Time: 45 mins**

1)  **Creating a Swagger specification** can be done with Apigee-127 on
    your local machine or in the cloud at
    [*http://apistudio.io*](http://apistudio.io), since both utilize the
    same Swagger editor. For this lab, we will assume that you are using
    [*http://apistudio.io*](http://apistudio.io). Click on Get Started
    to see the editor in action.

   a.  Copy the Swagger YAML located [here](https://raw.githubusercontent.com/gsjurseth/apigee-devjam/master/Lab%201%20-%20Designing%20APIs%20using%20Swagger/swagger.yaml)

   b.  Select the entire contents of the Swagger editor at API Studio
        in the browser and delete it. Paste the Swagger that you copied
        in its place.

   c.  On the right side of the screen you will see the generated
        documentation updated to reflect the API described by the
        Swagger that you just pasted.
        ![](./media/image5.png)   

   d.  On the right side of the Swagger editor, in the documentation
        view, scroll down to the Responses section and click the Try
        this operation button:
  
  
![](./media/image6.png)

a.  Scroll down past the request information in the yellow block, so
    that you can see the Send Request button. Click it to make an API
    request:\
    ![](./media/image7.png)

b.  View the response below the button. Note the three tabs (Rendered,
    Pretty, and Raw) and the ability to view the Headers and Body :

![](./media/image8.png)\
\
Please expand the Body section to view the entire response.

1)  **Creating an API proxy from the Swagger specification** can be done
    very easily in Apigee Edge.

    a.  In API Studio Edit the file and change the base path to
        /**{your\_baas\_org}**/sandbox/**{your\_initials}**, and replace
        **{your\_baas\_org}** with your BaaS org.

    b.  Copy the URL from the address bar in API Studio but replace the final '#' with /spec. (it will be of
        the form **playground.apistudio.io/XXXXXX/spec)**

    c.  Open up a browser tab and log in to http://enterprise.apigee.com

    d.  From the Organization drop-down in the top-right corner, select
        the organization assigned to you.

    e.  From the Environment drop-down, select ‘test’

    f.  From the main menu, select APIs → API Proxies

![](./media/image9.png)

a.  To create a new API proxy, select the + API Proxy button to add a
    new proxy.

![](./media/image10.png)

a.  We are going to create a ‘Reverse Proxy’. This is the most common
    type of API Proxy and allows us to route requests to backend
    services, and we are going to do this using OpenAPI. Hit the **Use
    OpenAPI** button in the Reverse proxy section.

> ![](./media/image11.png)

a.  Paste in the URL that you copied from API Studio, replace the
    **\#/** at the end of the URL with **spec**, and hit the **Apply**
    button, and then hit the **Next** button (in the bottom left corner)

> ![](./media/image12.png)

a.  On the Build a Proxy form that is displayed, provide information
    needed to generate the API proxy

> ![](./media/image13.png)
>
> Proxy Name: **{your\_initials}\_hotels**
>
> Project Base Path: **/v1/{your\_initials}\_hotels**
>
> Existing API:
> **https://api.usergrid.com/{your-BaaS-org}/sandbox/hotels**
>
> Description: **Façade to the Baas hotel data collection**
>
> Features: **None**
>
> **Note**: Replace **{your-BaaS-org}** with the actual name of your API
> BaaS organization.
>
> **Example:** If you name is ‘John Doe’, your API proxy name would be
> ‘jd\_hotels’. We will follow this naming convention throughout the
> DevJam.

a.  Leave the defaults on the next **Flows** screen, hit **Next** to
    continue

> ![](./media/image14.png)

a.  On the next screen select **Pass through (none)** as the
    Authorization scheme and hit **Next**

> ![](./media/image15.png)

a.  Leave the defaults on the next **Virtual Hosts** screen, hit
    **Next** to continue

> ![](./media/image16.png)

a.  Ensure that the ‘test’ checkbox is ticked on the Build screen and
    hit **Build and Deploy**

> ![](./media/image17.png)

a.  Once the proxy has been deployed, click on the **view
    {your\_initials}\_hotel proxy in the editor** link

> ![](./media/image18.png)

a.  Review the information on the resulting API Proxy page

> ![](./media/image19.png)

**Summary**

That completes our first hands-on lesson. In this short lab, you learned
the fundamentals of API design, creating Swagger specification for an
API also understood how to create an API proxy in Apigee Edge from an
existing Swagger specification.

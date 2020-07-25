# STC Tech Night #1 - Strapi

Welcome to STC Tech Night #1 🥳!

Here, we will learn about one of the most trending open-source CMS --- Strapi! Strapi is a flexible, open-source Headless CMS that gives developers the freedom to choose their favorite tools and frameworks while also allowing editors to easily manage and distribute their content.

Before we jump straight into the session, allow me to introduce ourself, do watch this short 1 minute video to know more 🎇!

[![intro video](/assets/banner.png)](https://www.youtube.com/watch?v=aBNvCoJP-ag)

Without further ado, let's get started!

The slides for this session is [here](https://slides.com/rainchai/deck-e89862), alternatively, you can download it [here](/slides.html)

WHAT'S INCLUDED FOR THE SESSION:

- [x] Creating new data model
- [x] Creating relationship between models
- [x] Simple authentication
- [x] Simple endpoint accessing

WHAT'S NOT INCLUDED FOR THE SESSION:

- [ ] A zero to master lecture
- [ ] File upload
- [ ] Overriding endpoint handler
- [ ] Setting up with external database (Using sqllite for now)

## Table of content 📄

1. [Demo](#demo)

    1.1 [Installation](#installation)

    1.2 [API Endpoints](#apiendpoints)
    - [Types of content](#typesofcontent)
    - [Creating a new collection type](#collectiontype)
    - [New entry](#newentry)
    - [Accessing endpoints](#accessingendpoint)

    1.3 [Roles and permissions](#rolesandpermissions)
    - [Access from public](#accessfrompublic)
    - [Create a new user](#createuser)

    1.4 [Continuing demo](##adjustmodel)
    - [Adjusting collection types model](#adjustmodel)

2. [Conclusion](#conclusion)

## Demo <a name="demo"></a>

A recorded session link will be inserted here after the event, if you prefer to watch the recorded session to follow the demo, feel free and go ahead! Otherwise, you may follow the step-by-step explaination below.

In this demo, we will be covering few features of Strapi 3.0:

1. [API Endpoints](#apiendpoints)
2. [Roles and permissions](#rolesandpermissions)

> Never have a lack of goals.
--- Lou Holtz

Let's start to learn by using an example, this is what we are going to have when we call the endpoint:

![goal](/assets/goal.png)

- One school can have many students

But before we jump into the topic, let's download and get strapi up and running!

<br>

### Installation <a name="installation"></a>

Because Strapi is written fully in javascript, hence it is necessary to have [nodejs](https://nodejs.org/en/) installed, go ahead and install if you haven't!

After you have your nodejs installed, open up your terminal and run:

```bash
npx create-strapi-app <YOUR PREFERRED FOLDER NAME> --quickstart
```

![install-1](/assets/install-1.jpg)

Hit enter and it should start creating a quickstart application.

> `--quickstart` use sqllite as default database, if you wish to have custom configuration, you can do it by overriding file in the future, or simply remove the --quickstart flag. see more at [https://strapi.io/documentation/v3.x/concepts/configurations.html](https://strapi.io/documentation/v3.x/concepts/configurations.html)

Grab your coffee and take a short break! Usually it will take a few while to download depending on your internet bandwidth, it's around few hundreds MB 😴.

You should see this once the strapi server is up and running

![install-2](/assets/install-2.jpg)

and an admin portal pop-up on your browser on `http://localhost:1337/admin`

![install-3](/assets/install-3.jpg)

Hurray! We had done our first module! 🎉

Just enter your favourite username and password (Don't use admin admin! 😜) and hit the "Ready to start" button!

----

### API Endpoints <a name="apiendpoints"></a>

We had done our installation and we are ready to create our first model!

But before that, let me explain what are the kind of model you can have in strapi...

<br>

#### Types of content <a name="typesofcontent"></a>

Now if you go and click on the `PLUGINS` -> `Content-Types Builder`, you can see there are 3 type of content you can create:

![api-1](/assets/api-1.jpg)

1. Collection type - Best for model `like user, restaurant, food, etc..`
2. Single type - Best for pages. `Like dashboard, home page, about us, etc...`
3. Component - Best for reusable model, `like Slots in the Schedule`, component **can't be** a standalone endpoint, it can only be attached to collection type and single type.

<br>

#### Creating a new collection type <a name="collectiontype"></a>

Click on the `PLUGINS` -> `Content-Types Builder` -> `COLLECTION TYPES` -> `Create new collection type`, and you should see a pop-up modal like this:

![api-2](/assets/api-2.jpg)

Type `School` and click `Continue`

Click on `Text` and enter `title`

![api-3](/assets/api-3.jpg)

Click `Finish`

Click `Save`

<br>

#### Adding new entry <a name="newentry"></a>

Now you had created your first model! Congrats 😁 You may continue and explore other kind of fields you can have in Strapi, but we will continue the flow for now

Let's go and create a school!

Click `COLLECTION TYPES` -> `Schools`

![api-4](/assets/api-4.jpg)

This is where you can see all the school entry, we haven't create any for now which is why it is empty.

Click on `Add new School` on your right.

Enter `Sunway Tech Club` on the `Title` field and hit `Save`!

You should now see an entry on your dashboard

![api-5](/assets/api-5.jpg)

<br>

#### Accessing endpoints <a name="accessingendpoint"></a>

You can now access the `School` model by going `http://localhost:1337/schools` (Do note it has an `s`)

All of the endpoints are created following [Open API Specification](https://swagger.io/specification/#:~:text=Introduction,or%20through%20network%20traffic%20inspection.)

You can take a look at Strapi documentation on the convention way of how the APIs are constructed [here](https://strapi.io/documentation/v3.x/content-api/api-endpoints.html#endpoints)

Now if we go to `http://localhost:1337/schools`, it's essentially open a `GET` request to get all entries of `School`.

Let's take a look on the endpoint...

![api-6](/assets/api-6.png)

Oops! What is this!! 😱 Did I do anything wrongly??

![api-7](/assets/api-7.jpg)
> source: [https://www.azquotes.com/quote/1486006](https://www.azquotes.com/quote/1486006)

Haha fret not! This is actually the expected behaviour, because:

> [you should receive a 403 error because you are not allowed, as Public user, to access to the articles (schools in our case).](https://strapi.io/documentation/3.0.0-beta.x/guides/auth-request.html#fetch-articles:~:text=you%20should%20receive%20a%20403%20error,user%2C%20to%20access%20to%20the%20articles.)

By default, Strapi will block all the request from anywhere unless you specify the permissions from the role.

In this case, we are accessing from `Public` role (Request without token, coming from nowhere).

----

### Roles and permissions <a name="rolesandpermissions"></a>

The issue above can be resolved by adjusting the permissions of what a request coming from `Public` can do!

Let's focus on the third built-in plugin: Roles & Permissions.

![roles-1](/assets/roles-1.jpg)

<br>

#### Access from public <a name="accessfrompublic"></a>

Let's click on the `Public`, we are going to focus on the `Application` section.

So what do we want to grant the access for schools? For now, we only allow the public to perform read operations.

To do this, we can check the `count`, `find`, `findOne` checboxes.

![roles-2](/assets/roles-2.jpg)

Do you notice that when you check the checkbox, on the right side you can see a "Bound route to..."?

By default, `count` operation is bounted to `/schools/count`, this means that by going to that endpoints, you will get the count of all the entries.

count: `/schools/count`
find: `/schools/`
findOne: `/schools/:id` - the :id is to replace with the entry id

Now you can hit `Save`.

Let's go back to `http://localhost:1337/schools`!

You should see this as the response now!

![roles-3](/assets/roles-3.png)

Hurray! It worked!

<br>

#### Roles

You may refer to [https://strapi.io/documentation/3.0.0-beta.x/plugins/users-permissions.html#concept](https://strapi.io/documentation/3.0.0-beta.x/plugins/users-permissions.html#concept) for more information about this plugin!

#### Creating a new user <a name="createuser"></a>

In order for us to create a new user, we can either use the admin portal, or, send a `POST` request to `/auth/local/register`.

It is an endpoint generated by the `Roles & Permissions` built-in plugin.

let's do it! I will be creating an user with an username of `Test1` and email of `test@test.com`

![roles-4](/assets/roles-4.jpg)

As a result of success, Strapi will send you back with a response contain a [JSON Web Token](https://jwt.io/)

![roles-5](/assets/roles-5.png)

We can use the token, attached in the request header in future when we only want to let user to access certain content.

You can learn more about authentication [here](https://strapi.io/documentation/v3.x/plugins/users-permissions.html#authentication)

#### Adjusting collection types model <a name="adjustmodel">

Now we want to add the user we just created to `School`, but right now the `School` model has no relation with `User` model.

We can adjust it by going to `PLUGINS` -> `Content-Types Builder` -> `School` -> `Add another field`

![roles-6](/assets/roles-6.jpg)

We will choose `Relation` for this case

- One school can have many students

In order for us to add a relation between `School` and `User`, we need to click on the dropdown menu and choose `User`

![roles-7](/assets/roles-7.jpg)

The current relation is **One School has one User**, we can click on the most right type of relation, which is **One School has many Users**, it sounds exactly like what we want!

We can rename the field name (on the school side) to students:

![roles-8](/assets/roles-8.jpg)

Hit on the `Finish` button and `Save`!

Let's head back to the `COLLECTION TYPES` -> `Schools`!

Select the only school we have, on your right side you can choose to add a student, choose `Test1`!

![roles-9.jpg](/assets/roles-9.jpg)

Go to `http://localhost:1337/schools` and we can see the student now!

🥳 You had completed the demo, this is just the start of your journey!

----

### Conclusion <a name="conclusion"></a>

There are a lot more that I did not covered in the demo above, but I do strongly recommend you to take a look into their [official documentation website](https://strapi.io/documentation/3.0.0-beta.x/getting-started/introduction.html#what-is-strapi).

Complete the whole documentation will only take you probably few days, the benefits you can from learning it definitely justify the amount of time you will be spending on it! 😎

if you had found any issue in the demo, do feel free to approach to us on our [Facebook page](https://facebook.com/sunwaytechclub) or open an issue [here](/issues), I will try to resolve it as soon as possible for you!

And --- that sums up the session for today, I hope you like it and do feel free to approach to us to have a session just like this, but from you 🔥!

# Contribute to Greenpress

Greenpress is developed using micro services, and you can contribute to a single micro-service while still relying on the stable builds of the other micro services.

## Preparations

Greenpress is developed in Node.js, containarized with Docker, and version controlled using git. You will need to have all three installed on your development machine in order to contribute to the Greenpress platform. _Note: On Linux and Mac, Git is pre-installed. If your development machine is Windows based, you will need to install Git as well._

To start your development environment, start by following the [getting started](https://docs.greenpress.info/guide/getting-started.html#installation) guide.

<!-- need to install node.js and docker. -->

##

## Contributor environment

In your local project's directory, create a subfolder called `dev`, and navigate to that subfolder. The `dev` subfolder is already preconfigured in the `.gitignore` file, as each micro-service is expected to be developed independently.

Make sure your local project is not running by running `greenpress stop`.

Fork the repository of the micro-service you wish to contribute to (we will refer to the `admin-panel` micro service in this guide), and clone it using `git clone git@github.com:[USERNAME]/admin-panel.git` or `git clone https://github.com/[USERNAME]/admin-panel.git` where [USERNAME] is your Github username. Your `dev` folder should now contain a subfolder called `admin-panel`, and your project tree should look like this (for a newly created project):

> my-app/ \
> **├── dev** \
> **│   └── admin-panel** \
> **│   &emsp;&emsp;└── ...** \
> ├── compose \
> ├── Dockerfile \
> ├── greenpress.config.js \
> ├── LICENSE \
> ├── node_modules \
> ├── package.json \
> ├── package-lock.json \
> └── README.md

Navigate into the newly cloned subfolder, and run:

```bash
$ yarn install
```

or

```bash
$ npm install
```

##

## Configuration

In the project's parent directory, create a [configuration file](https://docs.greenpress.info/guide/greenpress-configuration.html#the-config-file) named `greenpress.config.js`, and copy the following code into it:

```js
const IS_PROD = process.env.NODE_ENV === "production";

module.exports = {
  admin: "/dev/admin-panel/server.js",

  scripts: {
    admin:
      process.env.ADMIN_SERVICE_SCRIPT || IS_PROD
        ? "./admin/server.js"
        : "cd dev/admin-panel && npm run serve",
  },
};
```

This configuration file will be used to direct the development build to the local clone of the micro-service fork.

Your project tree should now look like this:

> my-app/ \
> **├── dev** \
> **│   └── admin-panel** \
> **│   &emsp;&emsp;└── ...** \
> ├── compose \
> ├── Dockerfile \
> ├── greenpress.config.js \
> ├── LICENSE \
> ├── node_modules \
> ├── package.json \
> ├── package-lock.json \
> ├── README.md \
> **_└── greenpress.config.js_**

Now, in your prjoect's main folder run:

```bash
$ greenpress start dev
```

##

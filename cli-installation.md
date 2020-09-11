# Installation

Vermillion cli helps developers to create a working application out of the box.
It has many useful commands like generating files for our vermillion app.

To install the cli we just need to run the following command:

```bash
npm install -g vermillion-cli
```

After installing the cli, we can verify if the installation is a success by running the following command:

```bash
vm --version
```

If the installation is a success it should display the version of the vermillion-cli installed in your machine.

We can find help with the cli using the `vm --help` command.

We can now start creating our new vermillion project by running this command:

```bash
vm new my-app
```

The syntax of the command above is `vm <command> <project name>` where "new" is the command and "my-app" is the project name.
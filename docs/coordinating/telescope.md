# Telescope

The [RCOS website](https://rcos.io) is now run using [Telescope](https://github.com/rcos/Telescope/). More documentation will be added here as more features are added to Telescope.

## Direct Access

 Sometimes it's necessary to have direct access to the RCOS database (in circumstances where Telescope does not have support yet or otherwise). This can be achieved using the Hasura console. 

To open the Hasura console, clone the [rcos-data](https://github.com/rcos/rcos-data) repository, and run inside it: 

```sh
hasura console --admin-secret xxxxxxxxxxxxxxxxxxxxxxxx 
```

Where the admin secret is the "Hasura Admin Secret" from the [RCOS Leadership Bitwarden](../passwords). 


# What's all that stuff in the `.ddev` directory?

It can be a little confusing trying to understand all the things that are in the project's `.ddev` directory, so here it is all on one place. Note that you may have some directories or files that are not listed here - they may be added from custom services. For example, if you see a `solr` directory, it probably pertains to a custom `solr` add-on service.

* `apache` directory: Apache configuration for those using `webserver_type: apache-fpm`. There are docs and the default configuration in there. See [apache customization docs](../extend/customization-extendibility.md#providing-custom-apache-configuration).
* `commands` subdirectories: Contains DDEV shell commands (both built-in and custom) that can run on the host or inside any container. See [docs](../extend/custom-commands.md).
* `config.yaml` file: This is the basic configuration file for the project. Take a look at the comments below for suggestions about things you can do, or look in [docs](../configuration/config_yaml.md)).
* `config.*.yaml` files: You can add configuration here that overrides the  config in the `config.yaml`. This is nice for situations where one developer's project needs one-off configuration. For example, you could turn on or off `nfs-mount-enabled` or `mutagen-enabled` or use a different database type. By default, these are gitignored, so will not get checked in. See [docs](../extend/customization-extendibility.md#extending-configyaml-with-custom-configyaml-files)
* `db-build` directory: Can be used to provide a custom Dockerfile for the database container.
* `db_snapshots` directory: This is where snapshots go when you `ddev snapshot`. If you don't need these backups, you can delete anything there at any time. See [snapshot docs](../basics/cli-usage.md#snapshotting-and-restoring-a-database).
* `docker-compose.*.yaml` files: Advanced users can provide their own services or service overrides using `docker-compose.*.yaml` files. See [custom compose files](../extend/custom-compose-files.md) and[additional services](../extend/additional-services.md). Also see the many examples in [ddev-contrib](https://github.com/drud/ddev-contrib).
* `homeadditions` directory: Anything you put in the `homeadditions` directory (including both files and directories) will be copied into the web container on startup. This lets you easily override the default home directory contents (`.profile`, `.bashrc`, `.composer`, `.ssh`) or anything you want to put in there. It could also include scripts that you want to have easily available inside the container. (Note that you can do the same thing globally in `~/.ddev/homeadditions`.) See [homeadditions docs](../extend/in-container-configuration.md).
* `mutagen` directory: contains `mutagen/mutagen.yml` where you can override the default mutagen configuration. See [mutagen docs](../install/performance.md#advanced-mutagen-configuration-options).
* `mysql` directory: contains optional `mysql` or `mariadb` configuration. See [mysql docs](../extend/customization-extendibility.md#providing-custom-mysqlmariadb-configuration-mycnf).
* `nginx` directory: (deprecated) can be used for add-on nginx snippets.
* `nginx_full` directory: Contains the nginx configuration used by the web container, which can be customized following the instructions there. See [providing custom nginx configuration](../extend/customization-extendibility.md#providing-custom-nginx-configuration).
* `postgres` directory: contains `postgres/postgresql.conf` which can be edited if needed (and remove the `#ddev-generated` line at the top to take it over.)
* `providers` directory: Contains examples and implementations showing ways to configure DDEV so `ddev pull` can work. You can use `ddev pull` with hosting providers like Acquia or Platform.sh or Pantheon and also can use it with local files or custom database/files sources. See [providers docs](../providers/index.md)
* `web-build` directory: You can add a custom Dockerfile that adds things into the docker image used for your web container. See [Customizing images](../extend/customizing-images.md).
* `xhprof` directory: Contains the `xhprof_prepend.php` file that can be used to customize xhprof behavior for different types of website. See [xhprof profiling](../debugging-profiling/xhprof-profiling.md).

## Things not to look at or mess with :)

The hidden files (that begin with a "." are not intended to be fiddled with, and are hidden for that reason, and most are regenerated (and thus overwritten) on every `ddev start`:

* `.dbimageBuild` directory: The generated Dockerfile used to customize the db container on first start.
* `.ddev-docker-compose-base.yaml`: The base docker-compose file used to describe a project.
* `.ddev-docker-compose-full.yaml`: This is the result of preprocessing `.ddev-docker-compose-base.yaml` using `docker-compose config`. Mostly it replaces environment variables with their values.
* `.gitignore`: The `.gitignore` is generated by DDEV and should generally not be edited or checked in. (It gitignores itself to make sure you don't check it in.) It's generated on every `ddev start` and will change as DDEV versions change, so if you check it in by accident it will always be showing changes that you don't need to see in `git status`.
* `.global_commands`: This is a temporary directory that is used to get global commands available inside a project. You shouldn't ever have to look there.
* `.homeadditions`: This is a temporary directory used to consolidate global `homeadditions` with project-level `homeadditions`. You shouldn't ever have to look here.
* `.webimageBuild` directory: The generated Dockerfile used to customize the web container on first start.
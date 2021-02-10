# Introduction 
TODO: Give a short introduction of your project. Let this section explain the objectives or the motivation behind this project. 

# Getting Started
TODO: Guide users through getting your code up and running on their own system. In this section you can talk about:
1.	Installation process
2.	Software dependencies
3.	Latest releases
4.	API references

# Build and Test
TODO: Describe and show how to build your code and run the tests. 

# Contribute
TODO: Explain how other users and developers can contribute to make your code better. 

If you want to learn more about creating good readme files then refer the following [guidelines](https://docs.microsoft.com/en-us/azure/devops/repos/git/create-a-readme?view=azure-devops). You can also seek inspiration from the below readme files:
- [ASP.NET Core](https://github.com/aspnet/Home)
- [Visual Studio Code](https://github.com/Microsoft/vscode)
- [Chakra Core](https://github.com/Microsoft/ChakraCore)

# Template

## db-template

### Prerequisites for adding build server
1.  Create agent on server where db server resides.
    1.  The agent should run as SEK\azuredevopsbuild.
    2.  SEK\azuredevopsbuild should be added to the Users group.
    3.  SEK\azuredevopsbuild should not be permitted for remote logon.
    4.  SEK\azuredevopsbuild should be granted "Logon as a service" permissions.
2.  Add capability db-server, value db server name, to agent.
3.  Add SEK\azuredevopsbuild (or other ad user if necessary) in the SQL Server. Should have the following permissions:
    1.  dbcreator (server role),
    2.  VIEW SERVER STATE.
4.  Run script database/tSQLt/PrepareServer.sql on db server (only needed if server version >= 2017).
5.  Create logon trigger, script database/CreateLogonTrigger.sql, mutatis mutandis if needed.

### Prerequisites for adding system (repo)

#### New system
1.  Add variable group with name equals to application name. Should contain variables with name = ENV (TESTx, Preprod, Prod), value = db server name.

#### Existing system
1.  Add variable group with name equals to application name. Should contain variables with name = ENV (TESTx, Preprod, Prod), value = db server name.
2.  If wanted, move all existing backups to the Azdo folder, see db-build.
    1.  Preparation: Restore database, add sek\azuredevopsbuild to db_owner role, backup database.
    2.  Folder structure is {azdo root}\\{application name}\\{dev\master}\\{version ordinal}-{build number}.
    3.  Name of database is {application name}-{database name}-{dev\master}-{version ordinal}-{build number}.bak.
    
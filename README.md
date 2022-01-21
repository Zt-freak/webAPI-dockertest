## First SQL Server container
1. Run `docker run -e "docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=yourStrong(!)Password" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-CU14-ubuntu-20.04` in command prompt
2. this creates a docker image and a container. The container is started.
3. Test connection in Azure Data Studio
    - Connection type: Microsoft SQL Server
    - Server: localhost, 1433
    - Authentication type: SQL Login
    - User name: sa
    - Password: yourStrong(!)Password
    - Remember password: true
    - Database: <Default>
    - Server group: <Default>
4. It works! OwO
## Second SQL Server container
1. Docker image already exists.
2. Run `docker run -e "docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=yourStrong(!)Password" -p 11433:11433 -d mcr.microsoft.com/mssql/server:2019-CU14-ubuntu-20.04` in command prompt
3. This creates a container.
4. Test connection in Azure Data Studio
    - Connection type: Microsoft SQL Server
    - Server: localhost, 11433
    - Authentication type: SQL Login
    - User name: sa
    - Password: yourStrong(!)Password
    - Remember password: true
    - Database: <Default>
    - Server group: <Default>
5. Failed
```
Microsoft.Data.SqlClient.SqlException (0x80131904): A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: TCP Provider, error: 0 - An existing connection was forcibly closed by the remote host.)
 ---> System.ComponentModel.Win32Exception (10054): An existing connection was forcibly closed by the remote host.
   at Microsoft.Data.SqlClient.SqlInternalConnection.OnError(SqlException exception, Boolean breakConnection, Action`1 wrapCloseInAction)
   at Microsoft.Data.SqlClient.TdsParser.ThrowExceptionAndWarning(TdsParserStateObject stateObj, Boolean callerHasConnectionLock, Boolean asyncClose)
   at Microsoft.Data.SqlClient.TdsParserStateObject.ThrowExceptionAndWarning(Boolean callerHasConnectionLock, Boolean asyncClose)
   at Microsoft.Data.SqlClient.TdsParserStateObject.ReadSniError(TdsParserStateObject stateObj, UInt32 error)
   at Microsoft.Data.SqlClient.TdsParserStateObject.ReadSniSyncOverAsync()
   at Microsoft.Data.SqlClient.TdsParserStateObject.TryReadNetworkPacket()
   at Microsoft.Data.SqlClient.TdsParser.ConsumePreLoginHandshake(Boolean encrypt, Boolean trustServerCert, Boolean integratedSecurity, Boolean& marsCapable, Boolean& fedAuthRequired)
   at Microsoft.Data.SqlClient.TdsParser.Connect(ServerInfo serverInfo, SqlInternalConnectionTds connHandler, Boolean ignoreSniOpenTimeout, Int64 timerExpire, Boolean encrypt, Boolean trustServerCert, Boolean integratedSecurity, Boolean withFailover, SqlAuthenticationMethod authType)
   at Microsoft.Data.SqlClient.SqlInternalConnectionTds.AttemptOneLogin(ServerInfo serverInfo, String newPassword, SecureString newSecurePassword, Boolean ignoreSniOpenTimeout, TimeoutTimer timeout, Boolean withFailover)
   at Microsoft.Data.SqlClient.SqlInternalConnectionTds.LoginNoFailover(ServerInfo serverInfo, String newPassword, SecureString newSecurePassword, Boolean redirectedUserInstance, SqlConnectionString connectionOptions, SqlCredential credential, TimeoutTimer timeout)
   at Microsoft.Data.SqlClient.SqlInternalConnectionTds.OpenLoginEnlist(TimeoutTimer timeout, SqlConnectionString connectionOptions, SqlCredential credential, String newPassword, SecureString newSecurePassword, Boolean redirectedUserInstance)
   at Microsoft.Data.SqlClient.SqlInternalConnectionTds..ctor(DbConnectionPoolIdentity identity, SqlConnectionString connectionOptions, SqlCredential credential, Object providerInfo, String newPassword, SecureString newSecurePassword, Boolean redirectedUserInstance, SqlConnectionString userConnectionOptions, SessionData reconnectSessionData, Boolean applyTransientFaultHandling, String accessToken, DbConnectionPool pool)
   at Microsoft.Data.SqlClient.SqlConnectionFactory.CreateConnection(DbConnectionOptions options, DbConnectionPoolKey poolKey, Object poolGroupProviderInfo, DbConnectionPool pool, DbConnection owningConnection, DbConnectionOptions userOptions)
   at Microsoft.Data.ProviderBase.DbConnectionFactory.CreateNonPooledConnection(DbConnection owningConnection, DbConnectionPoolGroup poolGroup, DbConnectionOptions userOptions)
   at Microsoft.Data.ProviderBase.DbConnectionFactory.<>c__DisplayClass48_0.<CreateReplaceConnectionContinuation>b__0(Task`1 _)
   at System.Threading.Tasks.ContinuationResultTaskFromResultTask`2.InnerInvoke()
   at System.Threading.ExecutionContext.RunInternal(ExecutionContext executionContext, ContextCallback callback, Object state)
--- End of stack trace from previous location ---
   at System.Threading.Tasks.Task.ExecuteWithThreadLocal(Task& currentTaskSlot, Thread threadPoolThread)
--- End of stack trace from previous location ---
   at Microsoft.SqlTools.ServiceLayer.Connection.ReliableConnection.ReliableSqlConnection.<>c__DisplayClass30_0.<<OpenAsync>b__0>d.MoveNext() in D:\a\1\s\src\Microsoft.SqlTools.ManagedBatchParser\ReliableConnection\ReliableSqlConnection.cs:line 312
--- End of stack trace from previous location ---
   at Microsoft.SqlTools.ServiceLayer.Connection.ConnectionService.TryOpenConnection(ConnectionInfo connectionInfo, ConnectParams connectionParams) in D:\a\1\s\src\Microsoft.SqlTools.ServiceLayer\Connection\ConnectionService.cs:line 559
ClientConnectionId:975b059b-1a7c-469f-8ec8-b6c0b220b8d1
Error Number:10054,State:0,Class:20
```
6. Try changing the "Trust server cetrificate" property.
7. Same exception
8. Run `docker run -e "docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=yourStrong(!)Password" -p 11433:1433 -d mcr.microsoft.com/mssql/server:2019-CU14-ubuntu-20.04` in command prompt.
9. This creates a container.
10. Test connection in Azure Data Studio
    - Connection type: Microsoft SQL Server
    - Server: localhost, 11433
    - Authentication type: SQL Login
    - User name: sa
    - Password: yourStrong(!)Password
    - Remember password: true
    - Database: <Default>
    - Server group: <Default>
11. Success!

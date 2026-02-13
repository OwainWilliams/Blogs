# Detailed Error messages on Azure

To enable detailed errors, you can use the _ASPNETCORE\_DETAILEDERRORS_ environment variable or configure the application to always show detailed error pages.

Example: Using ASPNETCORE\_DETAILEDERRORS

Add the following configuration to your _web.config_ file when hosting on IIS:

```
<configuration>
 <system.webServer>
   <aspNetCore processPath="dotnet" arguments=".\YourApp.dll">
     <environmentVariables>
       <environmentVariable name="ASPNETCORE_DETAILEDERRORS" value="true" />
     </environmentVariables>
   </aspNetCore>
 </system.webServer>
</configuration>
```

Example: Developer Exception Page in Code

In your _Startup.cs_ or _Program.cs_, enable the **Developer Exception Page** for the Development environment:

```
var app = builder.Build();
if (app.Environment.IsDevelopment())
{
   app.UseDeveloperExceptionPage();
}
else
{
   app.UseExceptionHandler("/Error");
   app.UseHsts();
}
app.Run();
```



This ensures that detailed error pages are shown only during development.

Important Considerations

1. **Environment-Specific Configuration**: Always restrict detailed error messages to the Development environment. Exposing them in Production can lead to security risks.
2. **Custom Error Pages**: For Production, use _UseExceptionHandler_ to redirect users to a custom error page.
3. **Testing**: Test your error-handling setup thoroughly to ensure no sensitive information is leaked.

By following these practices, you can debug effectively during development while maintaining security in production.

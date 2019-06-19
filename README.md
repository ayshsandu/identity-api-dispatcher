# identity-api-dispatcher

Aggregates the API implementations from [identity-user-api](https://github.com/ayshsandu/identity-user-api/) and 
[identity-server-api](https://github.com/ayshsandu/identity-server-api/) builds a single webapp inorder to expose the 
multiple API endpoints in WSO2 Identity Server. 

*  Refer [identity-user-api](https://github.com/ayshsandu/identity-user-api/) repository for the implementation 
of user APIs

*  Refer [identity-server-api](https://github.com/ayshsandu/identity-server-api/) repository for the implementation 
of server APIs

#### Exposing a new API

1. Add the dependency of the API implementation into the dependencies section of [parent.pom](https://github.com/ayshsandu/identity-api-dispatcher/blob/master/pom.xml#L121)
2. Include the dependency of the API implementation into the dependencies section of [parent.pom](https://github.com/ayshsandu/identity-api-dispatcher/blob/master/components/org.wso2.carbon.identity.api.dispatcher/pom.xml)
3. Open the [beans.xml](https://github.com/ayshsandu/identity-api-dispatcher/blob/master/components/org.wso2.carbon.identity.api.dispatcher/src/main/webapp/WEB-INF/beans.xml)

    ```
    
    components
    │   └── org.wso2.carbon.identity.api.dispatcher
    │       ├── pom.xml
    │       ├── src
    │       │   └── main
    │       │       └── webapp
    │       │           ├── META-INF
    │       │           └── WEB-INF
    │       │               ├── beans.xml
    │       │               └── web.xml
    ```
    
4. Add the API implementation from [identity-user-api](https://github.com/ayshsandu/identity-user-api/) or 
[identity-server-api](https://github.com/ayshsandu/identity-server-api/) under the corresponding `server` tag.

    ```
    <jaxrs:server id="server" address="/server/v1">
            <jaxrs:serviceBeans>
                <bean class="org.wso2.carbon.identity.rest.api.server.challenge.v1.ChallengesApi"/>
            </jaxrs:serviceBeans>
            <jaxrs:providers>
                <bean class="com.fasterxml.jackson.jaxrs.json.JacksonJsonProvider"/>
            </jaxrs:providers>
        </jaxrs:server>
        <jaxrs:server id="users" address="/users/v1">
            <jaxrs:serviceBeans>
                <bean class="org.wso2.carbon.identity.rest.api.user.association.v1.UsersApi"/>
                <bean class="org.wso2.carbon.identity.rest.api.user.challenge.v1.UserIdApi"/>
                <bean class="org.wso2.carbon.identity.rest.api.user.challenge.v1.MeApi"/>
            </jaxrs:serviceBeans>
            <jaxrs:providers>
                <bean class="com.fasterxml.jackson.jaxrs.json.JacksonJsonProvider"/>
            </jaxrs:providers>
        </jaxrs:server>
    ```
5. Build the component.

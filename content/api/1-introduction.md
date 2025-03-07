---
title: "Introduction"
metaTitle: "Introduction"
metaDescription: "Palette API Introduction"
icon: "graph"
hideToC: false
fullWidth: false
hiddenFromNav: false
hideToCSidebar: false
---
import {Intro, IntroButtons} from "shared/components"
import {Layout} from "shared"
import InfoBox from "shared/components/InfoBox"

<Intro>

# Palette APIs

</Intro>

Spectro Cloud Palette platform capabilities are exposed via REST APIs, providing a subset of features that comply with open application programming interface (API) standards. 

### APIs and External Resources 
Palette interacts with external-facing utility tools such as Terraform to provision, change, and manage your environment automatically and efficiently.

# Paths

Every API's URI has the prefix of the version and the Palette resource, such as: `v1/spectroclusters/...`

# Authentication
Palette supports two types of user authentication methods: 

### Using Authorization Token
  * All requests must be authenticated with an API token that are passed using the HTTP request header `Authorization`. 
  * Activated users can use the `/auth/authenticate` API to authenticate and obtain the Authorization token. 
  * Every authorization token is valid for 15 min. 
  * To refresh the token use [this GET call](https://docs.spectrocloud.com/api/v1/auth/): `GET /v1/auth/refresh/{token}` 
  
### Using the API Key
Palette enables secure authentication and authorization for API with the help of API Keys. This is the method of accessing the API without referring to the actual user credentials. The API key will be part of individual API requests to identify and authorize the request. This is a relatively more straight forward method of authentication. The API Key is passed using HTTP request header in the following format:
  * Key: ApiKey
  * Value: API key copied from the Palette Console. E.g. QMOI1ZVKVIoW6LM6uXqSWFPsjmt0juvl

[Read More...](/user-management/user-authentication/#usingapikey)         
# Requests

All requests are in the `JSON` format. In general, the request payload has three sections: *metadata, spec and status*.

* *Metadata* consists of common attributes for all the resources such as ids, names, creation timestamps etc. 
* *Spec* consists of attributes that define the resource
* *Status* contains the status information of the resource. The API does not support creating or modifying the status section. 

<InfoBox>
Certain update request schema have restricted spec resource definition and certain fields like uid, creation timestamp are not allowed to be modified post creation.
</InfoBox>

| HTTP Method | Documentation |
| --- | --- |
| POST | To create a resource or a sub-resource. |
| PUT | To update the resource or a sub-resource. The PUT request will overwrite the existing resource data. |
| PATCH | To add, modify, remove a specific attribute or sub-resource within a resource. |
| DELETE | To delete the resource. |

# Response Codes

The API returns standard HTTP response codes:

| HTTP Code | Description |
| --- | --- |
| 200 | For a successful response. The response payload will vary depending upon the API. Refer the respective API response schema. |
| 201 | For a successful resource creation. The response payload contains the uid of the created resource. |
| 204 | Response without any content for a successful operation. These operations include update, delete and the other actions on the resource. |
| 400 | Bad request. The request does not adhere to the API request payload schema. |
| 401 | Missing authorization token or invalid authorization token. |
| 403 | The API operation is forbidden for the user. |
| 404 | The resource or the dependent resource is not found for the operation. |
| 500 | Operational error. For 500 error code, the server responds with an explicit error code and an error message. |

# Palette API Lifecycle
Palette API will remain backward compatible indefinitely until deprecation. To keep up with the API lifecycle, we expose the state or phase the API is in—*Production*, *Sunsetting* or *Deprecated*. 
### Production
While in the Production stage, the Palette and Terraform APIs will work as intended and expected. 
### Sunsetting
As the API moves toward retirement, whether being replaced or no longer being supported, a notice is included in the documentation with the intent and a cut-off date. A notice is shared within three months to the date of deprecation as a countdown till the end date along with the recommendation of what API to use instead.
### Deprecated
When an API is no longer supported nor recommended to use, we indicate its state and include a tag as deprecated. The API documentation will continue to be available as a subsection of deprecated APIs.

**Note**: This API lifecycle also applies to external-facing tools such as Terraform and will be managed, accordingly.

# Versioning

The version information is part of the API URI like `v1alpha1`, `v1`. Future APIs will increment the version, leaving the earlier version API intact. The existing API request and response schema will undergo changes like adding new attributes or query parameters with backward compatibility of earlier schema. While advancing to the next version, ample notice to migrate to the new API will be provided.

# Scope

Palette supports applications to operate under [**Tenant** and **Project**](/user-management/palette-rbac#accessmodes) scope. The resources can be logically grouped as projects and the API requests. These resources within a project should carry the ProjectUid in the context. The project scope can be specified in the API request as an HTTP header with the key as `ProjectUid` and value as the &lt;Project Uid&gt; The `ProjectUid` needs to be specified for a request to be applied under the project scope.

**Example**:

While creating a cloud account under a specific project, the request should have the `ProjectUid in the http header.` If the request is submitted without the `ProjectUid` by default, it will be considered a Tenant Scope request.


# Pagination

The resources list APIs are limited to 50 items and pagination has to be performed to retrieve the complete resources list. The list API response contains `listMeta` with the `continue` token. The pagination can be performed based on the presence of the `continue` token value, and the subsequent request can be performed with the `continue` token as query parameter to paginate the rest of the resource items.

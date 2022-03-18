# Sonae MC RESTful API

`id`\</a\>"\>[Github
Repository](https://github.com/sonaemc/api-guidelines)

id

\</a\>"\>

![API Guilt Logo](assets/apis.jpg)

# Introduction

`id`\</a\>"\>Bit’s software architecture favours and centers around a
distributed system and decoupled services that provide functionality via
RESTful APIs with a JSON payload. Our APIs most purely express what our
systems do, and are therefore highly valuable business assets. Designing
high-quality, long-lasting APIs has become even more critical for us
since we started defining our platform strategy, which transforms Sonae
MC ecosystem into an expansive platform of platforms. Our strategy
emphasizes developing lots of public APIs for our business and external
business partners to use via internal and third-party applications.

`id`\</a\>"\>With this in mind, we’ve adopted "API First" as one of our
key engineering principles. Services development begins with API
definition outside the code and ideally involves ample peer-review
feedback to achieve high-quality APIs. API First encompasses a set of
quality-related standards and fosters a peer review culture including a
lightweight review procedure. We encourage our teams to follow them to
ensure that our APIs:

  - are easy to understand and learn

  - are general and abstracted from specific implementation and use
    cases

  - are robust and easy to use

  - have a common look and feel

  - follow a consistent RESTful style and syntax

  - are consistent with other teams’ APIs and our global architecture

`id`\</a\>"\>Ideally, all SOnae MC APIs will look like the same author
created them.

## Conventions used in these guidelines

`id`\</a\>"\>The requirement level keywords "MUST", "MUST NOT",
"REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",
"MAY", and "OPTIONAL" used in this document (case insensitive) are to be
interpreted as described in [RFC
2119](https://www.ietf.org/rfc/rfc2119.txt).

## What is this design standard?

`id`\</a\>"\>The purpose of our "RESTful API guidelines" is to define
standards to successfully establish "consistent API look and feel"
quality. This document is intended to be a reference point in the design
phase of a new API development process. The [API Guild \[internal
link](https://…/display/GUL/API+Guild)\] drafted and owns this document.
Teams are responsible to fulfill these guidelines during API design and
development and are encouraged to contribute to guideline evolution via
pull requests.

`id`\</a\>"\>These guidelines will, to some extent, remain work in
progress as our work evolves, but teams must confidently follow and
trust them.

`id`\</a\>"\>In case guidelines are changing, following rules apply:

  - existing APIs don’t have to be changed, but we recommend it

  - clients of existing APIs have to cope with these APIs based on
    outdated rules

  - **new APIs have to respect the current guidelines**

`id`\</a\>"\>Furthermore you should keep in mind that once an API
becomes public externally available, it has to be re-reviewed and
changed according to current guidelines - for sake of overall
consistency.

`id`\</a\>"\>The design standards defined in this document are both
data-agnostic (i.e. they don’t take into account the type of data being
consumed or produced), and programming language agnostic (i.e. they
don’t take into account the programming language being used).

`id`\</a\>"\>Instead, these design standards present common patterns
that are applicable to all API and integration scenarios and provides an
agreed upon view of how this scenario should be addressed.

`id`\</a\>"\>As such, this document does not need to be consumed and
understood in one sitting. Instead it can be used as a reference point
when facing a new API or integration scenario to understand the agreed
upon approach for implementation.

# Principles

## API design principles

`id`\</a\>"\>Comparing SOA web service interfacing style of SOAP vs.
REST, the former tend to be centered around operations that are usually
use-case specific and specialized. In contrast, REST is centered around
business (data) entities exposed as resources that are identified via
URIs and can be manipulated via standardized CRUD-like methods using
different representations, and hypermedia. RESTful APIs tend to be less
use-case specific and come with less rigid client / server coupling and
are more suitable for an ecosystem of (core) services providing a
platform of APIs to build diverse new business services. We apply the
RESTful web service principles to all kind of application (micro-)
service components, independently from whether they provide
functionality via the internet or intranet.

  - We prefer REST-based APIs with JSON payloads

  - We prefer systems to be truly RESTful \[1\]

`id`\</a\>"\>An important principle for API design and usage is Postel’s
Law, aka [The Robustness
Principle](http://en.wikipedia.org/wiki/Robustness_principle) (see also
[RFC 1122](https://tools.ietf.org/html/rfc1122)):

  - Be liberal in what you accept, be conservative in what you send

`id`\</a\>"\>*Readings:* Some interesting reads on the RESTful API
design style and service architecture:

  - Article: [REST API Design - Resource
    Modeling](https://www.thoughtworks.com/de/insights/blog/rest-api-design-resource-modeling)

  - Article: [Richardson Maturity Model — Steps toward the glory of
    REST](https://martinfowler.com/articles/richardsonMaturityModel.html)

  - Book: [Irresistable APIs: Designing web APIs that developers will
    love](https://www.amazon.de/Irresistible-APIs-Designing-that-developers/dp/1617292559)

  - Book: [REST in Practice: Hypermedia and Systems
    Architecture](http://www.amazon.de/REST-Practice-Hypermedia-Systems-Architecture/dp/0596805829)

  - Book: [Build APIs You Won’t
    Hate](https://leanpub.com/build-apis-you-wont-hate)

  - Fielding Dissertation: [Architectural Styles and the Design of
    Network-Based Software
    Architectures](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)

## API as a product

`id`\</a\>"\>We are transforming from an ad-hoc API exposed set of
services to an expansive platform comprising a rich set of products
following a Software as a Platform (SaaP) model to support our growing
business and our business partners. As a company we want to deliver
products to our (internal and external) customers which can be consumed
like a service.

`id`\</a\>"\>Platform products provide their functionality via (public)
APIs; hence, the design of our APIs should be based on the API as a
Product principle:

  - Treat your API as product and act like a product owner

  - Put yourself into the place of your customers; be an advocate for
    their needs

  - Emphasize simplicity, comprehensibility, and usability of APIs to
    make them irresistible for client engineers

  - Actively improve and maintain API consistency over the long term

  - Make use of customer feedback and provide service level support

`id`\</a\>"\>Embracing *API as a Product* facilitates a service
ecosystem, which can be evolved more easily and used to experiment
quickly with new business ideas by recombining core capabilities. It
makes the difference between agile, innovative product service business
built on a platform of APIs and ordinary enterprise integration business
where APIs are provided as "appendix" of existing products to support
system integration and optimised for local server-side realization.

`id`\</a\>"\>Understand the concrete use cases of your customers and
carefully check the trade-offs of your API design variants with a
product mindset. Avoid short-term implementation optimizations at the
expense of unnecessary client side obligations, and have a high
attention on API quality and client developer experience.

`id`\</a\>"\>API as a Product is closely related to our [API First
principle](#100) (see next chapter) which is more focused on how we
engineer high quality APIs.

## API first

`id`\</a\>"\>API First is one of our engineering and architecture
principles. In a nutshell API First requires two aspects:

  - define APIs first, before coding its implementation, using a
    standard specification language

  - get early review feedback from peers and client developers

`id`\</a\>"\>By defining APIs outside the code, we want to facilitate
early review feedback and also a development discipline that focus
service interface design on…

  - profound understanding of the domain and required functionality

  - generalized business entities / resources, i.e. avoidance of use
    case specific APIs

  - clear separation of WHAT vs. HOW concerns, i.e. abstraction from
    implementation aspects — APIs should be stable even if we replace
    complete service implementation including its underlying technology
    stack

`id`\</a\>"\>Moreover, API definitions with standardized specification
format also facilitate…

  - single source of truth for the API specification; it is a crucial
    part of a contract between service provider and client users

  - infrastructure tooling for API discovery, API GUIs, API documents,
    automated quality checks

`id`\</a\>"\>Elements of API First are also this API Guidelines and a
standardized API review process as to get early review feedback from
peers and client developers. Peer review is important for us to get high
quality APIs, to enable architectural and design alignment and to
supported development of client applications decoupled from service
provider engineering life cycle.

`id`\</a\>"\>It is important to learn, that API First is **not in
conflict with the agile development principles** that we love and
defend. Service applications should evolve incrementally — and so its
APIs. Of course, our API specification will and should evolve
iteratively in different cycles; however, each starting with draft
status and *early* team and peer review feedback. API may change and
profit from implementation concerns and automated testing feedback. API
evolution during development life cycle may include breaking changes for
not yet productive features and as long as we have aligned the changes
with the clients. Hence, API First does *not* mean that you must have
100% domain and requirement understanding and can never produce code
before you have defined the complete API and get it confirmed by peer
review.

`id`\</a\>"\>On the other hand, API First obviously is in conflict with
the bad practice of publishing API definition and asking for peer review
after the service integration or even the service productive operation
has started. It is crucial to request and get early feedback — as early
as possible, but not before the API changes are comprehensive with focus
to the next evolution step and have a certain quality (including API
Guideline compliance), already confirmed via team internal reviews.

## How to apply the design standard

`id`\</a\>"\>Knowing how and when to apply the API Design Standards will
significantly influence the API Solution Design.

`id`\</a\>"\>Determining when to use the standard is based on the API
Category and the required level of abstraction required.

`id`\</a\>"\>An API will generally fall into one of the following
categories:

  - **System Level APIs**: These are low-level APIs that are exposed
    directly by an application.

  - **Domain Level APIs**: These are APIs composed of other System APIs
    through orchestration and choreography.

  - **Experience Level APIs**: These are APIs intended to ease the
    adoption of API integration between an organisation and its external
    consumers.

`id`\</a\>"\>If your API falls into the **System Level API** and is
custom developed, it is RECOMMENDED that you use the design standard as
this will assist in developing **Domain** or **Experience** level APIs
if they are required in future.

`id`\</a\>"\>If your API is a **Domain Level API**, you MUST apply the
design standard as more often than not, a domain level API will be
tailored for re-usability.

`id`\</a\>"\>If your API is an **Experience Level API**, then the design
standards MUST also be applied.

`id`\</a\>"\>This design standard itself does **NOT** apply to
third-party **System level APIs** such as those available as
‘out-of-the-box’ or as part of SaaS platform, e.g. Salesforce APIs.
However, the standard may apply if you were looking to re-expose these
APIs as experience level APIs for wider consumption.

# Definitions

## API

`id`\</a\>"\>In the context of this API Design Standard, an API
(Application Programming Interface) is defined as a RESTful API.

`id`\</a\>"\>A RESTful API is a style of communication between systems
where resources are defined by URI and its operations are defined by the
use of HTTP methods.

`id`\</a\>"\>A RESTful API adopts many HTTP standards such as response
codes and methods.

## Platforms & Domains

`id`\</a\>"\>The platform and domain for a service defines the grouping
of related functions within. **Platforms** are high level (e.g. a
platform like loyalty) while the **domains** are one level below (e.g.
customers). This way, we can have an API that belongs to the loyalty
platform and customer domain in order to access operations related to
customers that have a customer account.

`id`\</a\>"\>Platforms and domains are relevant when designing your URL
structure and are further covered in section URI Component Names.

## Operation

`id`\</a\>"\>To make use of any of the platforms, domains, resources and
resource identifiers, developers must make use of Operations.

`id`\</a\>"\>An operation is defined by the use of:

  - an HTTP method; and

  - a resource path.

`id`\</a\>"\>Examples:

GET /employees GET /employees/6df5a5e569a4 DELETE
/employees/6df5a5e569a4\</programlisting\>

# General guidelines

`id`\</a\>"\>The titles are marked with the corresponding labels: MUST,
SHOULD, MAY.

`id`\</a\>"\>You must follow the [API First Principle](#api-first), more
specifically:

  - You must define APIs first, before coding its implementation, [using
    OpenAPI as specification language](#101). This includes filling in
    all **bitprint** information.

  - You must design your APIs consistently with these guidelines;

  - You must call for early review feedback from peers and client
    developers, and apply our lightweight API review process for all
    component Domain and Experience APIs.

`id`\</a\>"\>We use the [OpenAPI
specification](http://swagger.io/specification/) as standard to define
API specification files. API designers are required to provide the API
specification using a single **self-contained YAML** file to improve
readability. You MUST use **OpenAPI 3.0** version.

`id`\</a\>"\>The API specification files are subject to version control
using our selected source code management system.

`id`\</a\>"\>You [must publish](#192) the component API specification
prior to the development and deployment of the implementing service,
and, hence, make it discoverable for the group via our API Portal.

`id`\</a\>"\>**Hint:** A good way to explore **Open API 3.0** is to
navigate through the [Open API specification mind
map](https://openapi-map.apihandyman.io/). To explore and
validate/evaluate existing APIs the [Swagger
Editor](https://editor.swagger.io/) may be a good starting point.

`id`\</a\>"\>Normally, API specification files must be
**self-contained**, i.e. files should not contain references to local or
remote content, e.g. `../fragment.yaml#/element` or `$ref:
'https://github.com/...'`. The reason is, that the content referred to
is *in general* **not durable** and **not immutable**. As a consequence,
the semantic of an API may change in unexpected ways.

`id`\</a\>"\>However, you may use remote references to resources
accessible by the following service URLs:

  - `https://github.com/sonaemc/api-guidelines/tree/main/models/{model}.yaml`
    – used to refer to guideline defined re-usable API fragments (see
    `{*}.yaml` files in
    [api-guidelines/models](https://github.com/sonaemc/api-guidelines/tree/main/models)
    for details).

`id`\</a\>"\>As we control these URLs, we ensure that their content is
**durable** and **immutable**. This allows to define API specifications
by using fragments published via this sources, as suggested in
[???](#151).

`id`\</a\>"\>In addition to the API Specification, it is good practice
to provide an API user manual to improve client developer experience,
especially of engineers that are less experienced in using this API. A
helpful API user manual typically describes the following API aspects:

  - API scope, purpose, and use cases

  - concrete examples of API usage

  - edge cases, error situation details, and repair hints

  - architecture context and major dependencies - including figures and
    sequence flows

`id`\</a\>"\>The user manual must be published online, e.g. via our
documentation hosting platform service, GHE pages, or specific team web
servers. Please do not forget to include a link to the API user manual
into the API specification using the `#/externalDocs/url` property.

`id`\</a\>"\>To avoid having to manage several artifacts, we decided to
include Bitprint information directly in the SPEC. This information is
the essence of our BitOps process and SHOULD be the first information
added to the spec file.

``` yaml
x-bitprint:
  version: 1.0.0
  id: UUID
  stream: digital
  team: swat
  support_stream: digital
  platform: ecommerce
  domain: payments
  name: v1-ecommerce-payments-transactions
  display_name: E-Commerce Payments API - Transactions
  lac: 0474
  business_unit: bit
  tier: 1
  developers:
    - username: developer_1@sonaemc.com
    - username: developer_2@sonaemc.com
  maintainers:
    - username: maintainer_1@sonaemc.com
  architects:
    - username: architect_1@sonaemc.com
  status: active / deprecated // optional => active by default
  audience: external-partners

openapi: 3.0.1
info:
  title:
    $ref: '{{/x-bitprint/name}}'
  version:
    $ref: '{{/x-bitprint/version}}'

servers:
- url: https://ecommerce.sonaemc-api.com/payments/v1

tags:
...
```

# Meta information

`id`\</a\>"\>API specifications must contain the following Open API meta
information to allow for API management:

  - `#/info/title` as (unique) identifying, functional descriptive name
    of the API

  - `#/info/version` to distinguish API specifications versions
    following [semantic rules](#116)

  - `#/info/description` containing a proper description of the API

  - `#/info/contact/{name,url,email}` containing the responsible team

`id`\</a\>"\>Open API allows to specify the API specification version in
`#/info/version`. To share a common semantic of version information we
expect API designers to comply to [Semantic
Versioning 2.0](http://semver.org/spec/v2.0.0.html) rules `1` to `8` and
`11` restricted to the format \<MAJOR\>.\<MINOR\>.\<PATCH\> for versions
as follows:

  - Increment the **MAJOR** version when you make **incompatible** or
    **breaking** API changes,

  - Increment the **MINOR** version when you add new functionality in a
    backwards-compatible manner, and

  - Increment the **PATCH** version when you make backwards-compatible
    bug fixes or editorial changes not affecting the functionality.

## MAJOR VERSION

`id`\</a\>"\>

`id`\</a\>"\>The minor and patch versions are NOT required in the URI as
the changes are backwards-compatible.

`id`\</a\>"\>With each new major version of the API the older versions
are required until all the consumers are uplifted to use the new
versions. This adds to the overall maintenance and support requirements.

`id`\</a\>"\>Using the gateway platform, identify consumers and
decommission older version(s) of the API with sufficient notification.

`id`\</a\>"\>When new major versions are published the older version
must be deprecated following the deprecation process in [API
Deprecation](#deprecation).

## Minor and Patch Documentation

`id`\</a\>"\>The OAS definition SHOULD also contain the minor and patch
version.

`id`\</a\>"\>The implementation version is the physical build version
that was created.

`id`\</a\>"\>For example:

| API implementation version | Change Type               | Version Change                                          |
| -------------------------- | ------------------------- | ------------------------------------------------------- |
| `1.29.01`                  | `Bug Fixes`               | `API implementation version will be changed to 1.29.02` |
| `1.29.xx`                  | `Backward Compatible`     | `API implementation version will be changed to 1.30.0`  |
| `1.29.xx`                  | `Non-Backward Compatible` | `API implementation version will be changed to 2.0.0`   |

# Security

`id`\</a\>"\>All APIs MUST be secured and support both of the following
methods:

1.  OAuth2 (**preferred method to be used by clients**)

2.  API key validation

`id`\</a\>"\>Implementations SHOULD use OAuth2.  
APIs MUST support both security methods in order to provide more options
to the consumers.

## SHOULD authenticate with OAuth2

`id`\</a\>"\>Every API endpoint **must** be secured using OAuth 2.0.
Please refer to the [Open API
Authentication](https://swagger.io/docs/specification/authentication/)
section on how to specify security definitions in your API.

`id`\</a\>"\>**Example**: Most of our services require a simple
authentication using the [Bearer
Authentication](https://swagger.io/docs/specification/authentication/bearer-authentication/)
pattern originally created as part of
[RFC 6750](https://tools.ietf.org/html/rfc6750) using JWT tokens
provided in each request by:

``` http
---
Auhorization: Bearer <token>
---
```

`id`\</a\>"\>The following code snippet shows how to define the security
scheme.

``` yaml
components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

## MAY authenticate with API key

`id`\</a\>"\>Usage of API keys is an option when OAuth2 is not possible
by the client

  - API keys MUST only be permitted when TLS is enabled.

  - A rotation policy for API Keys MUST be defined and communication to
    the clients must be guaranteed.

  - All approved API Keys MUST have a predefined sunset date

  - Clients must be aware that a new API Key will be provided in a
    timely manner, which will work in parallel with the previous one,
    given them time to make the necessary changes

  - API keys SHOULD NOT be included in the URL or query string.

  - API keys SHOULD be included in the HTTP header. This is because URLs
    and query strings may be saved by the client or server in
    unencrypted format by the browser or server application

# Compatibility

`id`\</a\>"\>Change APIs, but keep all consumers running. Consumers
usually have independent release lifecycles, focus on stability, and
avoid changes that do not provide additional value. APIs are contracts
between service providers and service consumers that cannot be broken
via unilateral decisions.

`id`\</a\>"\>There are two techniques to change APIs without breaking
them:

  - follow rules for compatible extensions

  - introduce new API versions and still support older versions
    ([???](#115))

`id`\</a\>"\>In most cases introducing new fields to an API or adding
new endpoints is a non-breaking change and can be introduced with a
patch version update.

`id`\</a\>"\>Should the API contract need to change in a manner that
breaks the consumers contract this MUST be communicated clearly.

1.  API Product owners MUST document the support lifespan for API
    services (e.g. how long they will be supported).

2.  New functionality MUST be introduced in a way that does not impact
    existing consumers.

3.  Any deprecation activities MUST be known to consumers prior to them
    being put into effect.

`id`\</a\>"\>API designers should apply the following rules to evolve
RESTful APIs for services in a backward-compatible way:

  - Add only optional, never mandatory fields.

  - Never change the semantic of fields (e.g. changing the semantic from
    customer-number to customer-id, as both are different unique
    customer keys)

  - Input fields may have (complex) constraints being validated via
    server-side business logic. Never change the validation logic to be
    more restrictive and make sure that all constraints are clearly
    defined in description.

  - Enum ranges can be reduced when used as input parameters, only if
    the server is ready to accept and handle old range values too. Enum
    range can be reduced when used as output parameters.

  - Enum ranges cannot be extended when used for output parameters —
    clients may not be prepared to handle it. However, enum ranges can
    be extended when used for input parameters.

  - Use `x-extensible-enum`, if range is used for output parameters and
    likely to be extended with growing functionality. It defines an open
    list of explicit values and clients must be agnostic to new values.

  - Support redirection in case an URL has to change 301 (Moved
    Permanently).

`id`\</a\>"\>Service clients should apply the robustness principle:

  - Be conservative with API requests and data passed as input, e.g.
    avoid to exploit definition deficits like passing megabytes of
    strings with unspecified maximum length.

  - Be tolerant in processing and reading data of API responses, more
    specifically…

`id`\</a\>"\>Service clients must be prepared for compatible API
extensions of service providers:

  - Be tolerant with unknown fields in the payload (see also Fowler’s
    ["TolerantReader"](http://martinfowler.com/bliki/TolerantReader.html)
    post), i.e. ignore new fields but do not eliminate them from payload
    if needed for subsequent `PUT` requests.

  - Be prepared that `x-extensible-enum` return parameter may deliver
    new values; either be agnostic or provide default behavior for
    unknown values.

  - Be prepared to handle HTTP status codes not explicitly specified in
    endpoint definitions. Note also, that status codes are extensible.
    Default handling is how you would treat the corresponding 2xx code
    (see [RFC 7231
    Section 6](https://tools.ietf.org/html/rfc7231#section-6)).

  - Follow the redirect when the server returns HTTP status code 301
    (Moved Permanently).

`id`\</a\>"\>Designers of service provider APIs should be conservative
and accurate in what they accept from clients:

  - Unknown input fields in payload or URL should not be ignored;
    servers should provide error feedback to clients via an HTTP 400
    response code.

  - Be accurate in defining input data constraints (like formats,
    ranges, lengths etc.) — and check constraints and return dedicated
    error information in case of violations.

  - Prefer being more specific and restrictive (if compliant to
    functional requirements), e.g. by defining length range of strings.
    It may simplify implementation while providing freedom for further
    evolution as compatible extensions.

`id`\</a\>"\>Not ignoring unknown input fields is a specific deviation
from Postel’s Law (e.g. see also  
[The Robustness Principle
Reconsidered](https://cacm.acm.org/magazines/2011/8/114933-the-robustness-principle-reconsidered/fulltext))
and a strong recommendation. Servers might want to take different
approach but should be aware of the following problems and be explicit
in what is supported:

  - Ignoring unknown input fields is actually not an option for `PUT`,
    since it becomes asymmetric with subsequent `GET` response and HTTP
    is clear about the `PUT` *replace* semantics and default roundtrip
    expectations (see [RFC 7231
    Section 4.3.4](https://tools.ietf.org/html/rfc7231#section-4.3.4)).
    Note, accepting (i.e. not ignoring) unknown input fields and
    returning it in subsequent `GET` responses is a different situation
    and compliant to `PUT` semantics.

  - Certain client errors cannot be recognized by servers, e.g.
    attribute name typing errors will be ignored without server error
    feedback. The server cannot differentiate between the client
    intentionally providing an additional field versus the client
    sending a mistakenly named field, when the client’s actual intent
    was to provide an optional input field.

  - Future extensions of the input data structure might be in conflict
    with already ignored fields and, hence, will not be compatible, i.e.
    break clients that already use this field but with different type.

`id`\</a\>"\>In specific situations, where a (known) input field is not
needed anymore, it either can stay in the API definition with "not used
anymore" description or can be removed from the API definition as long
as the server ignores this specific parameter.

`id`\</a\>"\>In a response body, you must always return a JSON object
(and not e.g. an array) as a top level data structure to support future
extensibility. JSON objects support compatible extension by additional
attributes. This allows you to easily extend your response and e.g. add
pagination later, without breaking backwards compatibility. See
[???](#161) for an example.

`id`\</a\>"\>Maps (see [???](#216)), even though technically objects,
are also forbidden as top level data structures, since they don’t
support compatible, future extensions.

`id`\</a\>"\>The Open API specification is not very specific on default
extensibility of objects, and redefines JSON-Schema keywords related to
extensibility, like `additionalProperties`. Following our compatibility
guidelines, Open API object definitions are considered open for
extension by default as per [Section 5.18
"additionalProperties"](http://json-schema.org/latest/json-schema-validation.html#rfc.section.5.18)
of JSON-Schema.

`id`\</a\>"\>When it comes to Open API, this means an
`additionalProperties` declaration is not required to make an object
definition extensible:

  - API clients consuming data must not assume that objects are closed
    for extension in the absence of an `additionalProperties`
    declaration and must ignore fields sent by the server they cannot
    process. This allows API servers to evolve their data formats.

  - For API servers receiving unexpected data, the situation is slightly
    different. Instead of ignoring fields, servers *may* reject requests
    whose entities contain undefined fields in order to signal to
    clients that those fields would not be stored on behalf of the
    client. API designers must document clearly how unexpected fields
    are handled for `PUT`, `POST`, and `PATCH` requests.

`id`\</a\>"\>API formats must not declare `additionalProperties` to be
false, as this prevents objects being extended in the future.

`id`\</a\>"\>Note that this guideline concentrates on default
extensibility and does not exclude the use of `additionalProperties`
with a schema as a value, which might be appropriate in some
circumstances, e.g. see [???](#216).

`id`\</a\>"\>Enumerations are per definition closed sets of values, that
are assumed to be complete and not intended for extension. This closed
principle of enumerations imposes compatibility issues when an
enumeration must be extended. To avoid these issues, we strongly
recommend to use an open-ended list of values instead of an enumeration
unless:

1.  the API has full control of the enumeration values, i.e. the list of
    values does not depend on any external tool or interface, and

2.  the list of value is complete with respect to any thinkable and
    unthinkable future feature.

`id`\</a\>"\>To specify an open-ended list of values use the marker
`x-extensible-enum` as follows:

``` yaml
delivery_methods:
  type: string
  x-extensible-enum:
    - PARCEL
    - LETTER
    - EMAIL
```

`id`\</a\>"\>**Note:** `x-extensible-enum` is not JSON Schema conform
but will be ignored by most tools.

`id`\</a\>"\>See [???](#240) about enum value naming conventions.

`id`\</a\>"\>When changing your RESTful APIs, do so in a compatible way
and avoid generating additional API versions. Multiple versions can
significantly complicate understanding, testing, maintaining, evolving,
operating and releasing our systems ([supplementary
reading](http://martinfowler.com/articles/enterpriseREST.html)).

`id`\</a\>"\>If changing an API can’t be done in a compatible way, then
create a new API version supported in parallel with the old API until
the defined sunset date (see [Deprecation](#deprecation)).

`id`\</a\>"\>Since a new major API version that results in deprecation
of a pre-existing API version can be a significant product investment,
API owners SHOULD justify the new major version before beginning
significant design and development work.

`id`\</a\>"\>API owners SHOULD explore all possible alternatives to
introducing a new major API version with the objective of minimizing the
impact on customers before deciding to introduce a new version.

`id`\</a\>"\>Topics RECOMMENDED to consider/validate before creating a
new major version:

id

\</a\>"\>

`id`\</a\>"\>**Business Case**

1.  Customer value delivered by new version that is not possible with
    existing version.

2.  Cost-benefit analysis of deprecated version versus the new version.

3.  Explanation of alternatives to introducing a new major version and
    why those were not chosen.

4.  If a backwards incompatible change is required to address a critical
    security issue, items 1 and 2 (above) are not required.

id

\</a\>"\>

`id`\</a\>"\>**API Design**

1.  A domain model of all resources in the new API version and how they
    compare to the domain model of the previous major API version.

2.  Description of APIs operations and use cases they implement.

3.  Definition of service level objectives for performance and
    availability that are equal or better to the major API version to be
    deprecated.

id

\</a\>"\>

`id`\</a\>"\>**Migration Strategy**

1.  Number of existing customers impacted; internal, external and
    partners.

2.  Communication and support plan to inform existing customers of new
    version, value and migration path.

# Deprecation

`id`\</a\>"\>Sometimes it is necessary to phase out an API endpoint, an
API version, or an API feature, e.g. if a field or parameter is no
longer supported or a whole business functionality behind an endpoint is
supposed to be shut down. As long as the API endpoints and features are
still used by consumers, these shutdowns are breaking changes and not
allowed. To progress the following deprecation rules have to be applied
to make sure that the necessary consumer changes and actions are well
communicated and aligned using *deprecation* and *sunset* dates.

`id`\</a\>"\>Before shutting down an API, version of an API, or API
feature the producer must make sure, that all clients have given their
consent on a sunset date. Producers should help consumers to migrate to
a potential new API or API feature by providing a migration manual and
clearly state the time line for replacement availability and sunset (see
also [???](#189)). Once all clients of a sunset API feature are
migrated, the producer may shut down the deprecated API feature.

`id`\</a\>"\>If the API is consumed by any external partner, the API
owner must define a reasonable time span that the API will be maintained
after the producer has announced deprecation. All external partners must
state consent with this after-deprecation-life-span, i.e. the minimum
time span between official deprecation and first possible sunset,
**before** they are allowed to use the API.

`id`\</a\>"\>The API deprecation must be part of the API specification.

`id`\</a\>"\>If an API endpoint (operation object), an input argument
(parameter object), an in/out data object (schema object), or on a more
fine grained level, a schema attribute or property should be deprecated,
the producers must set `deprecated: true` for the affected element and
add further explanation to the `description` section of the API
specification. If a future shut down is planned, the producer must
provide a sunset date and document in details what consumers should use
instead and how to migrate.

`id`\</a\>"\>Owners of an API, API version, or API feature used in
production that is scheduled for sunset must monitor the usage of the
sunset API, API version, or API feature in order to observe migration
progress and avoid uncontrolled breaking effects on ongoing consumers.
See also [???](#193).

`id`\</a\>"\>During the deprecation phase, the producer should add a
`Deprecation: <date-time>` (see [draft: RFC Deprecation HTTP
Header](https://tools.ietf.org/html/draft-ietf-httpapi-deprecation-header))
and - if also planned - a `Sunset: <date-time>` (see
[RFC 8594](https://tools.ietf.org/html/rfc8594#section-3)) header on
each response affected by a deprecated element (see [???](#187)).

`id`\</a\>"\>The `Deprecation` header can either be set to `true` - if a
feature is retired -, or carry a deprecation time stamp, at which a
replacement will become/became available and consumers must not on-board
any longer (see [???](#191)). The optional `Sunset` time stamp carries
the information when consumers latest have to stop using a feature. The
sunset date should always offer an eligible time interval for switching
to a replacement feature.

``` txt
Deprecation: Tue, 31 Dec 2024 23:59:59 GMT
Sunset: Wed, 31 Dec 2025 23:59:59 GMT
```

`id`\</a\>"\>If multiple elements are deprecated the `Deprecation` and
`Sunset` headers are expected to be set to the earliest time stamp to
reflect the shortest interval consumers are expected to get active.

`id`\</a\>"\>**Note:** adding the `Deprecation` and `Sunset` header is
not sufficient to gain client consent to shut down an API or feature.

`id`\</a\>"\>Clients should monitor the `Deprecation` and `Sunset`
headers in HTTP responses to get information about future sunset of APIs
and API features (see [???](#189)). We recommend that client owners
build alerts on this monitoring information to ensure alignment with
service owners on required migration task.

`id`\</a\>"\>Clients must not start using deprecated APIs, API versions,
or API features.  
If an API is marked for deprecation and there is no new major version
but a new client needs to use it, the deprecation decision SHOULD be
reviewed.  
Make sure the API lifecycle framework principles are followed.

# JSON guidelines

`id`\</a\>"\>These guidelines provides recommendations for defining JSON
data at Sonae MC. JSON here refers to
[RFC 7159](https://tools.ietf.org/html/rfc7159) (which updates
[RFC 4627](https://tools.ietf.org/html/rfc4627)), the "application/json"
media type and custom JSON media types defined for APIs. The guidelines
clarifies some specific cases to allow Sonae MC JSON data to have an
idiomatic form across teams and services.

`id`\</a\>"\>The first of the following guidelines are about property
names, the later ones about values.

`id`\</a\>"\>Names of arrays should be pluralized to indicate that they
contain multiple values. This implies in turn that object names should
be singular.

`id`\</a\>"\>Property names are restricted to ASCII strings. The first
character must be a letter, or an underscore, and subsequent characters
can be a letter, an underscore, or a number.

`id`\</a\>"\>(It is recommended to use `_` at the start of property
names only for keywords like `_links`.)

`id`\</a\>"\>Rationale: No established industry standard exists, but
many popular Internet companies prefer snake\_case: e.g. GitHub, Stack
Exchange, Twitter. Others, like Google and Amazon, use both - but not
only camelCase. It’s essential to establish a consistent look and feel
such that JSON looks as if it came from the same hand.

`id`\</a\>"\>Enumerations should be represented as `string` typed
OpenAPI definitions of request parameters or model properties. Enum
values (using `enum` or `x-extensible-enum`) need to consistently use
the upper-snake case format, e.g. `VALUE` or `YET_ANOTHER_VALUE`. This
approach allows to clearly distinguish values from properties or other
elements.

`id`\</a\>"\>**Note:** This does not apply where the actual exact values
are coming from some outside source, e.g. for language codes from
[ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes), or
when declaring possible values for [rule 137](#137) \[`sort`
parameter\].

`id`\</a\>"\>A "map" here is a mapping from string keys to some other
type. In JSON this is represented as an object, the key-value pairs
being represented by property names and property values. In Open API
schema (as well as in JSON schema) they should be represented using
additionalProperties with a schema defining the value type. Such an
object should normally have no other defined properties.

`id`\</a\>"\>The map keys don’t count as property names in the sense of
[rule 118](#118), and can follow whatever format is natural for their
domain. Please document this in the description of the map object’s
schema.

`id`\</a\>"\>Here is an example for such a map definition (the
`translations` property):

`id`\</a\>"\>\`\`\`yaml components: schemas: Message: description: A
message together with translations in several languages. type: object
properties: message\_key: type: string description: The message key.
translations: description: The translations of this message into several
languages. The keys are \[IETF BCP-47 language
tags\](<https://tools.ietf.org/html/bcp47>). type: object
additionalProperties: type: string description: the translation of this
message into the language identified by the key. \`\`\`

`id`\</a\>"\>An actual JSON object described by this might then look
like this: \`\`\`json { "message\_key": "color", "translations": { "de":
"Farbe", "en-US": "color", "en-GB": "colour", "eo": "koloro", "nl":
"kleur" } } \`\`\`

`id`\</a\>"\>Schema based JSON properties that are by design booleans
must not be presented as nulls. A boolean is essentially a closed
enumeration of two values, true and false.  
**If the content has a meaningful null value or, for some reason, can be
a null value**, strongly prefer to replace the boolean with enumeration
of named values or statuses - for example
accepted\_terms\_and\_conditions with true or false can be replaced with
terms\_and\_conditions with values yes, no and unknown.

`id`\</a\>"\>Open API 3.x allows to mark properties as `required` and as
`nullable` to specify whether properties may be absent (`{}`) or `null`
(`{"example":null}`). If a property is defined to be not `required` and
`nullable` (see [2nd row in Table below](#required-nullable-row-2)),
this rule demands that both cases must be handled in the exact same
manner by specification.

`id`\</a\>"\>The following table shows all combinations and whether the
examples are valid:

| required | nullable | {}    | {"example":null} |
| -------- | -------- | ----- | ---------------- |
| `true`   | `true`   | ✗ No  | ✔ Yes            |
| `false`  | `true`   | ✔ Yes | ✔ Yes            |
| `true`   | `false`  | ✗ No  | ✗ No             |
| `false`  | `false`  | ✔ Yes | ✗ No             |

`id`\</a\>"\>While API designers and implementers may be tempted to
assign different semantics to both cases, we explicitly decide
**against** that option, because we think that any gain in
expressiveness is far outweighed by the risk of clients not
understanding and implementing the subtle differences incorrectly.

`id`\</a\>"\>As an example, an API that provides the ability for
different users to coordinate on a time schedule, e.g. a meeting, may
have a resource for options in which every user has to make a `choice`.
The difference between *undecided* and *decided against any of the
options* could be modeled as *absent* and `null` respectively. It would
be safer to express the `null` case with a dedicated [Null
object](https://en.wikipedia.org/wiki/Null_object_pattern), e.g. `{}`
compared to `{"id":"42"}`.

`id`\</a\>"\>Moreover, many major libraries have somewhere between
little to no support for a `null`/absent pattern (see
[Gson](https://stackoverflow.com/questions/48465005/gson-distinguish-null-value-field-and-missing-field),
[Moshi](https://github.com/square/moshi#borrows-from-gson),
[Jackson](https://github.com/FasterXML/jackson-databind/issues/578),
[JSON-B](https://developer.ibm.com/articles/j-javaee8-json-binding-3/)).
Especially strongly-typed languages suffer from this since a new
composite type is required to express the third state. Nullable
`Option`/`Optional`/`Maybe` types could be used but having nullable
references of these types completely contradicts their purpose.

`id`\</a\>"\>**The only exception** to this rule is JSON Merge Patch
[RFC 7396](https://tools.ietf.org/html/rfc7396)) which uses `null` to
explicitly indicate property deletion while absent properties are
ignored, i.e. not modified.

`id`\</a\>"\>Empty array values can unambiguously be represented as the
empty list, `[]`.

`id`\</a\>"\>Dates and date-time properties should end with `_at` to
distinguish them from boolean properties which otherwise would have very
similar or even identical names:

  - `created_at` rather than `created`,

  - `modified_at` rather than `modified`,

  - `occurred_at` rather than `occurred`, and

  - `returned_at` rather than `returned`.

`id`\</a\>"\>Use the date and time formats defined by
[RFC 3339](https://tools.ietf.org/html/rfc3339#section-5.6):

  - for "date" use strings matching `date-fullyear "-" date-month "-"
    date-mday`, for example: `2021-05-28`

  - for "date-time" use strings matching `full-date "T" full-time`, for
    example `2021-05-28T14:07:17Z`

`id`\</a\>"\>Note that the [Open API
format](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#data-types)
"date-time" corresponds to "full-date" in the RFC and `2021-05-28` for a
date. Both are specific profiles, a subset of the international standard
[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).

`id`\</a\>"\>A zone offset may be used (both, in request and
responses) — this is simply defined by the standards. However, we
encourage restricting dates to UTC and without offsets. For example
`2021-05-28T14:07:17Z` rather than `2021-05-28T14:07:17+00:00`. From
experience we have learned that zone offsets are not easy to understand
and often not correctly handled. Note also that zone offsets are
different from local times that might be including daylight saving time.
Localization of dates should be done by the services that provide user
interfaces, if required.

`id`\</a\>"\>When it comes to storage, all dates should be consistently
stored in UTC without a zone offset. Localization should be done locally
by the services that provide user interfaces, if required.

`id`\</a\>"\>Sometimes it can seem data is naturally represented using
numerical timestamps, but this can introduce interpretation issues with
precision, e.g. whether to represent a timestamp as 1460062925,
1460062925000 or 1460062925.000. Date strings, though more verbose and
requiring more effort to parse, avoid this ambiguity.

`id`\</a\>"\>Schema based JSON properties that are by design durations
and intervals could be strings formatted as recommended by
[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)([Appendix A of
RFC 3339 contains a
grammar](https://tools.ietf.org/html/rfc3339#appendix-A) for durations).

# Data formats

`id`\</a\>"\>Use JSON ([RFC 7159](https://tools.ietf.org/html/rfc7159))
to represent structured (resource) data passed with HTTP requests and
responses as body payload. The JSON payload MUST use a JSON object as
top-level data structure (if possible) to allow for future extension.
This also applies to collection resources, where you ad-hoc would use an
array — see also [???](#110).

`id`\</a\>"\>Additionally, the JSON payload must comply to the more
restrictive Internet JSON
([RFC 7493](https://tools.ietf.org/html/rfc7493)), particularly

  - [Section 2.1](https://tools.ietf.org/html/rfc7493#section-2.1) on
    encoding of characters, and

  - [Section 2.3](https://tools.ietf.org/html/rfc7493#section-2.3) on
    object constraints.

`id`\</a\>"\>As a consequence, a JSON payload must

  - use [`UTF-8`
    encoding](https://tools.ietf.org/html/rfc7493#section-2.1)

  - consist of [valid Unicode
    strings](https://tools.ietf.org/html/rfc7493#section-2.1), i.e. must
    not contain non-characters or surrogates, and

  - contain only [unique member
    names](https://tools.ietf.org/html/rfc7493#section-2.3) (no
    duplicate names).

`id`\</a\>"\>Use the standard media type name `application/json` (or
`application/problem+json` for [???](#176)) as content type (or accept
header) information for JSON payload.

`id`\</a\>"\>Non-JSON media types may be supported, if you stick to a
business object specific standard format for the payload data, for
instance, image data format (JPG, PNG, GIF), document format (PDF, DOC,
ODF, PPT), or archive format (TAR, ZIP).

`id`\</a\>"\>Generic structured data interchange formats other than JSON
(e.g. XML, CSV) may be provided, but only additionally to JSON as
default format using content negotiation, for specific use cases where
clients may not interpret the payload structure.

`id`\</a\>"\>Exposing binary data using an alternative media type is
generally preferred. See [the rule above](#168).

`id`\</a\>"\>If an alternative content representation is not desired
then binary data should be embedded into the JSON document as a
`base64url`-encoded string property following [RFC 7493
Section 4.4](https://tools.ietf.org/html/rfc7493#section-4.4).

`id`\</a\>"\>[JSON
Schema](https://json-schema.org/understanding-json-schema/reference/string.html#format)
and [Open
API](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#data-types)
define several data formats, e.g. `date`, `time`, `email`, and `url`,
based on ISO and IETF standards. The following table lists these formats
including additional formats useful in an e-commerce environment. You
**should** use these formats, whenever applicable.

| `type`    | `format`            | Specification                                                                         | Example                            |
| --------- | ------------------- | ------------------------------------------------------------------------------------- | ---------------------------------- |
| `integer` | [`int32`](#171)     |                                                                                       | `7721071004`                       |
| `integer` | [`int64`](#171)     |                                                                                       | `772107100456824`                  |
| `integer` | [`bigint`](#171)    |                                                                                       | `77210710045682438959`             |
| `number`  | [`float`](#171)     | [IEEE 754-2008](https://en.wikipedia.org/wiki/IEEE_754)                               | `3.1415927`                        |
| `number`  | [`double`](#171)    | [IEEE 754-2008](https://en.wikipedia.org/wiki/IEEE_754)                               | `3.141592653589793`                |
| `number`  | [`decimal`](#171)   |                                                                                       | `3.141592653589793238462643383279` |
| `string`  | [`bcp47`](#170)     | [BCP 47](https://tools.ietf.org/html/bcp47)                                           | `"en-DE"`                          |
| `string`  | `byte`              | [RFC 7493](https://tools.ietf.org/html/rfc7493)                                       | `"dGVzdA=="`                       |
| `string`  | [`date`](#126)      | [RFC 3339](https://tools.ietf.org/html/rfc3339)                                       | `"2019-07-30"`                     |
| `string`  | [`date-time`](#126) | [RFC 3339](https://tools.ietf.org/html/rfc3339)                                       | `"2019-07-30T06:43:40.252Z"`       |
| `string`  | `email`             | [RFC 5322](https://tools.ietf.org/html/rfc5322)                                       | `"example@sonaemc.com"`            |
| `string`  | `gtin-13`           | [GTIN](https://en.wikipedia.org/wiki/Global_Trade_Item_Number)                        | `"5710798389878"`                  |
| `string`  | `hostname`          | [RFC 1034](https://tools.ietf.org/html/rfc1034)                                       | `"www.sonaemc.com"`                |
| `string`  | `ipv4`              | [RFC 2673](https://tools.ietf.org/html/rfc2673)                                       | `"104.75.173.179"`                 |
| `string`  | `ipv6`              | [RFC 2673](https://tools.ietf.org/html/rfc2673)                                       | `"2600:1401:2::8a"`                |
| `string`  | [`iso-3166`](#170)  | [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)                | `"DE"`                             |
| `string`  | [`iso-4217`](#173)  | [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)                                    | `"EUR"`                            |
| `string`  | [`iso-639`](#170)   | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)                    | `"de"`                             |
| `string`  | `json-pointer`      | [RFC 6901](https://tools.ietf.org/html/rfc6901)                                       | `"/items/0/id"`                    |
| `string`  | `password`          |                                                                                       | `"secret"`                         |
| `string`  | `regex`             | [ECMA 262](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf) | `"^[a-z0-9]+$"`                    |
| `string`  | [`time`](#126)      | [RFC 3339](https://tools.ietf.org/html/rfc3339)                                       | `"06:43:40.252Z"`                  |
| `string`  | `uri`               | [RFC 3986](https://tools.ietf.org/html/rfc3986)                                       | `"https://www.sonaemc.com/"`       |
| `string`  | `uri-template`      | [RFC 6570](https://tools.ietf.org/html/rfc6570)                                       | `"/users/\{id\}"`                  |
| `string`  | [`uuid`](#144)      | [RFC 4122](https://tools.ietf.org/html/rfc4122)                                       | `"e2ab873e-b295-11e9-9c02-..."`    |

`id`\</a\>"\>**Remark:** Please note that this list of standard data
formats is not exhaustive and everyone is encouraged to propose
additions.

## JSON payload

`id`\</a\>"\>Read more about date and time format in [???](#126).

## HTTP headers

`id`\</a\>"\>Http headers including the proprietary headers use the
[HTTP date format defined in
RFC 7231](https://tools.ietf.org/html/rfc7231#section-7.1.1.1).

`id`\</a\>"\>Use the following standard formats for country, language
and currency codes:

  - Country codes:
    [ISO 3166-1-alpha2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
    two letter country codes
    
      - Hint: It is "GB", not "UK"

  - Language codes:
    [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
    two letter language codes

  - Language variant tags: [BCP 47](https://tools.ietf.org/html/bcp47)
    
      - It is a compatible extension of
        [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes),
        providing additional information for language usage, like region
        (using
        [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)),
        variant, script and others.

  - Currency codes: [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)
    three letter currency codes

`id`\</a\>"\>Whenever an API defines a property of type `number` or
`integer`, the precision must be defined by the format as follows to
prevent clients from guessing the precision incorrectly, and thereby
changing the value unintentionally:

| type    | format  | specified value range                                                                          |
| ------- | ------- | ---------------------------------------------------------------------------------------------- |
| integer | int32   | integer between -231 and 231-1                                                                 |
| integer | int64   | integer between -263 and 263-1                                                                 |
| integer | bigint  | arbitrarily large signed integer number                                                        |
| number  | float   | [IEEE 754-2008/ISO 60559:2011](https://en.wikipedia.org/wiki/IEEE_754) binary32 decimal number |
| number  | double  | [IEEE 754-2008/ISO 60559:2011](https://en.wikipedia.org/wiki/IEEE_754) binary64 decimal number |
| number  | decimal | arbitrarily precise signed decimal number                                                      |

`id`\</a\>"\>The precision must be translated by clients and servers
into the most specific language types. E.g. for the following
definitions the most specific language types in Java will translate to
`BigDecimal` for `Money.amount` and `int` or `Integer` for the
`OrderList.page_size`:

``` yaml
components:
  schemas:
    Money:
      type: object
      properties:
        amount:
          type: number
          description: Amount expressed as a decimal number of major currency units
          format: decimal
          example: 99.95
       ...

    OrderList:
      type: object
      properties:
        page_size:
          type: integer
          description: Number of orders in list
          format: int32
          example: 42
```

# Common data types

`id`\</a\>"\>Definitions of data objects that are good candidates for
wider usage. Below you can find a list of common data types used in the
guideline:

  - [Problem object](#176)

`id`\</a\>"\>There exist a variety of field types that are required in
multiple places. To achieve consistency across all API implementations,
you must use common field names and semantics whenever applicable.

## Generic fields

`id`\</a\>"\>There are some data fields that come up again and again in
API data:

  - `id`: the identity of the object. If used, IDs must be opaque
    strings and not numbers. IDs are unique within some documented
    context, are stable and don’t change for a given object once
    assigned, and are never recycled cross entities.

  - `xyz_id`: an attribute within one object holding the identifier of
    another object must use a name that corresponds to the type of the
    referenced object or the relationship to the referenced object
    followed by `_id` (e.g. `partner_id` not `partner_number`, or
    `parent_node_id` for the reference to a parent node from a child
    node, even if both have the type `Node`).

  - `created_at`: when the object was created. If used, this must be a
    `date-time` construct.

  - `modified_at`: when the object was updated. If used, this must be a
    `date-time` construct.

  - `type`: the kind of thing this object is. If used, the type of this
    field should be a string. Types allow runtime information on the
    entity provided that otherwise requires examining the Open API file.

  - `ETag`: the [ETag](#182) of an [embedded sub-resource](#158). It may
    be used to carry the `ETag` for subsequent `PUT`/`PATCH` calls (see
    [ in result entities](#etag-in-result-entities)).

`id`\</a\>"\>Example JSON schema:

``` yaml
tree_node:
  type: object
  properties:
    id:
      description: the identifier of this node
      type: string
    created_at:
      description: when got this node created
      type: string
      format: 'date-time'
    modified_at:
      description: when got this node last updated
      type: string
      format: 'date-time'
    type:
      type: string
      enum: [ 'LEAF', 'NODE' ]
    parent_node_id:
      description: the identifier of the parent node of this node
      type: string
  example:
    id: '123435'
    created_at: '2017-04-12T23:20:50.52Z'
    modified_at: '2017-04-12T23:20:50.52Z'
    type: 'LEAF'
    parent_node_id: '534321'
```

`id`\</a\>"\>These properties are not always strictly necessary, but
making them idiomatic allows API client developers to build up a common
understanding of Sonae MC’s resources. There is very little utility for
API consumers in having different names or value types for these fields
across APIs.

## Pagination fields

`id`\</a\>"\>For iterating over collections (result sets) we propose to
either use cursors (see [???](#160)) or simple hypertext controls (see
[???](#161)). It is RECOMMENDED for the response body to include \_meta
and \_links fields to provide the client with appropriate information
about the result set, and for easy navigation within the collection. The
fields can also remove the need for clients to unnecessarily parse query
parameters to continue navigating the collection. To implement these in
a consistent way, we have defined a response page object pattern with
the following field semantics:

  - `_links`:the \_links object SHOULD include links for self, first,
    last, next and prev
    
      - `self`:the link or cursor in a pagination response or object
        pointing to the same collection object or page.
    
      - `first`: the link or cursor in a pagination response or object
        pointing to the first collection object or page.
    
      - `prev`: the link or cursor in a pagination response or object
        pointing to the previous collection object or page.
    
      - `next`: the link or cursor in a pagination response or object
        pointing to the next collection object or page.
    
      - `last`: the link or cursor in a pagination response or object
        pointing to the last collection object or page.

  - `_meta`:the \_meta object SHOULD Pagination responses should contain
    the following additional array field to transport the page content:

  - `items`: array of resources, holding all the items of the current
    page (`items` may be replaced by a resource name).

`id`\</a\>"\>To simplify user experience, the applied query filters may
be returned using the following field (see also `GET with body`):

  - `query`: object containing the query filters applied in the search
    request to filter the collection resource.

`id`\</a\>"\>As Result, the standard response page using [cursors](#160)
or [pagination links](#161) may be defined as follows:

``` yaml
ResponsePage:
  type: object
  required:
    - _links
    - _meta
  properties:
    _links:
      description: Links object model
      readOnly: true
      type: object
      required:
        - self
        - first
        - prev
        - next
        - last
      properties:
        self:
          description: Pagination link|cursor pointing to the current page.
          type: string
          format: uri | cursor
          readOnly: true
        first:
          description: Pagination link|cursor pointing to the first page.
          type: string
          format: uri | cursor
          readOnly: true
        prev:
          description: Pagination link|cursor pointing to the previous page.
          type: string
          format: uri | cursor
          readOnly: true
        next:
          description: Pagination link|cursor pointing to the next page.
          type: string
          format: uri | cursor
          readOnly: true
        last:
          description: Pagination link|cursor pointing to the last page.
          type: string
          format: uri | cursor
          readOnly: true
    _meta:
      description: Metadata object model
      readOnly: true
      type: object
      properties:
        processing_time:
          type: string
          description: "The processing time for this request in human readable format."
          example: "10 milliseconds"
        processing_time_ms:
          type: integer
          description: "The processing time for this request in milliseconds."
          example: 10
        total_records:
          type: integer
          description: "Total number of the results which meets the search criteria."
          example: 38
        limit:
          type: integer
          description: "The number of records per page."
          example: 10
        page_record_count:
          type: integer
          description: "Number of records in the current page"
          example: 8

    _query:
      description: >
        Object containing the query filters applied to the collection resource.
      type: object
      properties: ...

    items:
      description: Array of collection items.
      type: array
      required: false
      items:
        type: ...
```

`id`\</a\>"\>**Note:** While you may support cursors for `next`, `prev`,
`first`, `last`, and `self` (see [Pagination
fields](#pagination-fields)), it is best practice to replace these with
links in favor of [???](#161).

# API naming

`id`\</a\>"\>Hostnames in APIs must conform to the naming as follows:

``` bnf
<hostname>             ::= <gateway-hostname> | <application-hostname>

<gateway-hostname>  ::= <platform-name>.sonaemc-apis.com
<application-hostname> ::= <platform-name>-<application-name>.sonaemc-apps.com
```

`id`\</a\>"\>Example:

``` http
/shipment-orders/{shipment-order-id}
```

`id`\</a\>"\>This applies to concrete path segments and not the names of
path parameters. For example `{shipment_order_id}` would be ok as a path
parameter.

`id`\</a\>"\>Examples:

customer\_number, order\_id, billing\_address\</programlisting\>

`id`\</a\>"\>Usually, a collection of resource instances is provided (at
least the API should be ready here). The special case of a *resource
singleton* must be modeled as a collection with cardinality 1 including
definition of `maxItems` = `minItems` = 1 for the returned `array`
structure to make the cardinality constraint explicit.

`id`\</a\>"\>**Exception:** the *pseudo identifier* `self` used to
specify a resource endpoint where the resource identifier is provided by
authorization information (see [???](#143)).

`id`\</a\>"\>In most cases, all resources provided by a service are part
of the base path.

`id`\</a\>"\>For non-public/system APIs exposed in our gateway to be
used in the context of a specific platform/domain,

`id`\</a\>"\>We see API’s base path as a part of deployment variant
configuration. Therefore, this information has to be declared in the
[server
object](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#server-object).

`id`\</a\>"\>You must not specify paths with duplicate or trailing
slashes, e.g. `/customers//addresses` or `/customers/`. As a
consequence, you must also not specify or use path variables with empty
string values.

`id`\</a\>"\>**Reasoning:** Non standard paths have no clear semantics.
As a result, behavior for non standard paths varies between different
HTTP infrastructure components and libraries. This may leads to
ambiguous and unexpected results during request handling and monitoring.

`id`\</a\>"\>We recommend to implement services robust against clients
not following this rule. All services **should**
[normalize](https://en.wikipedia.org/wiki/URI_normalization) request
paths before processing by removing duplicate and trailing slashes.
Hence, the following requests should refer to the same resource:

``` http
GET /orders/{order-id}
GET /orders/{order-id}/
GET /orders//{order-id}
```

`id`\</a\>"\>**Note:** path normalization is not supported by all
framework out-of-the-box. Services are required to support at least the
normalized path while rejecting all alternatives paths, if failing to
deliver the same resource.

`id`\</a\>"\>If you provide query support for searching, sorting,
filtering, and paginating, you must stick to the following naming
conventions:

  - `q`: default query parameter, e.g. used by browser tab completion;
    should have an entity specific alias, e.g. sku.

  - `sort`: comma-separated list of fields (as defined by [???](#154))
    to define the sort order. To indicate sorting direction, fields may
    be prefixed with `+` (ascending) or `-` (descending), e.g.
    /sales-orders?sort=+id.

  - `fields`: field name expression to retrieve only a subset of fields
    of a resource. See [???](#157) below.

  - `embed`: field name expression to expand or embedded sub-entities,
    e.g. inside of an article entity, expand silhouette code into the
    silhouette object. Implementing `embed` correctly is difficult, so
    do it with care. See [???](#158) below.

  - `offset`: numeric offset of the first element provided on a page
    representing a collection request. See [Pagination](#pagination)
    section below.

  - `cursor`: an opaque pointer to a page, never to be inspected or
    constructed by clients. It usually (encrypted) encodes the page
    position, i.e. the identifier of the first or last page element, the
    pagination direction, and the applied query filters to recreate the
    collection. See [Cursor-based pagination in RESTful
    APIs](#cursor-based-pagination) or [Pagination](#pagination) section
    below.

  - `limit`: client suggested limit to restrict the number of entries on
    a page. See [Pagination](#pagination) section below.

## Gateway API URI Breakdown

https://{platform}.sonaemc-apis.com/{domain}/v{N}/collection/resource-id?sort=asc
\\\_\_\_\_\_/\\\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_/\\\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_/\\\_\_\_\_\_\_\_/
| | | | scheme hostname path query\</programlisting\>

`id`\</a\>"\>The following table provides a breakdown of how to
construct the API URI.

| URI Element                 | Description                                                                                                                         | Example                                                                                                                                       |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `Protocol`                  | `All APIs MUST be exposed using HTTPS.`                                                                                             | `https://`                                                                                                                                    |
| `Hostname > Platform`       | `The platform of where the API endpoint will be exposed.`                                                                           | `e-commerce.sonaemc-apis.com`                                                                                                                 |
| `Path > system`             | `Only used for internal platform/domain APIs (replaces the Domain). The name of the system owner of the service/API being exposed.` | `e.g. /_system/retek`                                                                                                                         |
| `Path > Domain`             | `The information domain of the API that is desired to be accessed by the consumer.`                                                 | `e.g. /loyalty All APIs must belong to a given domain of information.`                                                                        |
| `Path > Version`            | `The version of the API that is desired to be accessed by the consumer.`                                                            | `e.g. /v1 All APIs must specify a version that follow the versioning scheme as specified in <<116,versioning>>.`                              |
| `Path > Collection`         | `The collection identifies a list of resources. The collection MUST be named using the plural representation of a noun.`            | `e.g. As part of the products API - a resource could be a list of products.`                                                                  |
| `Path > Resource`           | `The resource identifier which corresponds to an instance of the resource.`                                                         | `e.g. As part of the products API - if there was a specific product with id 1234. These details can be retrieved using GET /v1/products/1234` |
| `Query String > Parameters` | `Query parameters MUST NOT be used to transport payload or actual data.`                                                            | `See <<137>> for some examples.`                                                                                                              |

# Resources

## Resource

`id`\</a\>"\>In order to design a useful and clean API your system
should be broken down into logical groupings (often called Models or
Resources). In most cases the resources are the *nouns* of your system.

`id`\</a\>"\>In the example of an HR system, the resources are
*employees*, *positions* and *leave-requests*.

`id`\</a\>"\>By breaking systems down into these logical areas it allows
a clean separation of concerns (e.g. employee functions only work on
*employees* and only *employees* can apply for *leave-requests*). It
also ensures that each piece of data that is returned from your API is
the smallest that it needs to be to fulfil the client requirement (e.g.
when asking for *employees* you don’t also receive back
*family-members*).

## Resource Identifier

`id`\</a\>"\>Every resource that is available within your system (e.g.
every employee or every leave-request) must be identifiable uniquely
within the system. This is a key element of the RESTful style of APIs;
the ability to individually address any item within your system and
store these identifiers for later use.

| Name                | Example                                           |
| ------------------- | ------------------------------------------------- |
| `Numeric`           | `/employees/12389`                                |
| `String`            | `/country-codes/portugal`                         |
| `GUID`              | `/employees/0d047d80-eb69-4665-9395-6df5a5e569a4` |
| `Date (Short form)` | `/dates/2018-09-17`                               |

`id`\</a\>"\>As long as the identifier is unique within your application
it can be any string of characters or numbers.

`id`\</a\>"\>The resource identifier MUST be immutable. Primary keys or
Personally Identifiable Information (PII) MUST NOT be exposed. When
numeric IDs are used they MUST NOT be sequential e.g. it should not be
trivial to guess the next ID. If this is difficult to achieve, then it
is likely the API needs to be further abstracted from the underlying
data source.

## Representation

`id`\</a\>"\>A key concept in RESTful API design is the idea of the
representation of a resource at any particular time.

`id`\</a\>"\>When you ask the system for employee information you will
receive a representation of that employee e.g.

``` json
HTTP 1.1 GET /employees/john-smith
Accept: application/json

200 OK
Content-Type: application/json

{
  "name" : "John Smith",
  "employee_id" : "123456",
  "position" : "Manager",
  "on_leave" : false
}
```

`id`\</a\>"\>The intent is this representation can change over time as
the system and data within changes. A future call to this same endpoint
may yield a different representation possibly if the employee is now on
leave or their position within the organisation has changed.

`id`\</a\>"\>It is also possible to request an entirely different
representation of this same resource if the system supports it. For
example, there may be a case where you require a PDF version of this
employee and this could be facilitated with a request for a different
representation through the *Accept* header:

``` json
HTTP 1.1 GET /employees/john-smith
Accept: application/pdf

200 OK
Content-Type: application/pdf

...<BINARY CODE>...
```

`id`\</a\>"\>More information about representations and how to support
them is provided in the [Hypermedia](#hypermedia) section of this
document.

`id`\</a\>"\>REST is all about your resources, so consider the domain
entities that take part in web service interaction, and aim to model
your API around these using the standard HTTP methods as operation
indicators. For instance, if an application has to lock articles
explicitly so that only one user may edit them, create an article lock
with `PUT` or `POST` instead of using a lock action.

`id`\</a\>"\>Request:

``` http
PUT /article-locks/{article-id}
```

`id`\</a\>"\>The added benefit is that you already have a service for
browsing and filtering article locks.

`id`\</a\>"\>An API should contain the complete business processes
containing all resources representing the process. This enables clients
to understand the business process, foster a consistent design of the
business process, allow for synergies from description and
implementation perspective, and eliminates implicit invisible
dependencies between APIs.

`id`\</a\>"\>In addition, it prevents services from being designed as
thin wrappers around databases, which normally tends to shift business
logic to the clients.

`id`\</a\>"\>As a rule of thumb resources should be defined to cover 90%
of all its client’s use cases. A *useful* resource should contain as
much information as necessary, but as little as possible. A great way to
support the last 10% is to allow clients to specify their needs for
more/less information by supporting filtering and [embedding](#157).

`id`\</a\>"\>The API describes resources, so the only place where
actions should appear is in the HTTP methods. In URLs, use only nouns.
Instead of thinking of actions (verbs), it’s often helpful to think
about putting a message in a letter box: e.g., instead of having the
verb *cancel* in the url, think of sending a message to cancel an order
to the *cancellations* letter box on the server side.

`id`\</a\>"\>API resources represent elements of the application’s
domain model. Using domain-specific nomenclature for resource names
helps developers to understand the functionality and basic semantics of
your resources. It also reduces the need for further documentation
outside the API definition. For example, "sales-order-items" is superior
to "order-items" in that it clearly indicates which business object it
represents. Along these lines, "items" is too general.

`id`\</a\>"\>To simplify encoding of resource IDs in URLs, their
representation must only consist of ASCII strings using letters,
numbers, underscore, minus, colon, period, and - on rare occasions -
slash.

`id`\</a\>"\>**Note:** slashes are only allowed to build and signal
resource identifiers consisting of [compound keys](#241).

`id`\</a\>"\>**Note:** to prevent ambiguities of [unnormalized
paths](#136) resource identifiers must never be empty. Consequently,
support of empty strings for path parameters is forbidden.

`id`\</a\>"\>Some API resources may contain or reference sub-resources.
Embedded sub-resources, which are not top-level resources, are parts of
a higher-level resource and cannot be used outside of its scope.
Sub-resources should be referenced by their name and identifier in the
path segments as follows:

``` http
/resources/{resource-id}/sub-resources/{sub-resource-id}
```

`id`\</a\>"\>In order to improve the consumer experience, you should aim
for intuitively understandable URLs, where each sub-path is a valid
reference to a resource or a set of resources. For instance, if
`/partners/{partner-id}/addresses/{address-id}` is valid, then, in
principle, also `/partners/{partner-id}/addresses`,
`/partners/{partner-id}` and `/partners` must be valid. Examples of
concrete url paths:

``` http
/shopping-carts/de:1681e6b88ec1/items/1
/shopping-carts/de:1681e6b88ec1
/content/images/9cacb4d8
/content/images
```

`id`\</a\>"\>**Note:** resource identifiers may be build of multiple
other resource identifiers (see [???](#241)).

`id`\</a\>"\>**Exception:** In some situations the resource identifier
is not passed as a path segment but via the authorization information,
e.g. an authorization token or session cookie. Here, it is reasonable to
use **`self`** as *pseudo-identifier* path segment. For instance, you
may define `/employees/self` or `/employees/self/personal-details` as
resource paths —  and may additionally define endpoints that support
identifier passing in the resource path, like define `/employees/{id}`
or `/employees/{id}/personal-details`.

`id`\</a\>"\>If a resource is best identified by a *compound key*
consisting of multiple other resource identifiers, it is allowed to
reuse the compound key in its natural form containing slashes instead of
*technical* resource identifier in the resource path without violating
the above rule [???](#143) as follows:

``` http
/resources/{compound-key-1}[delim-1]...[delim-n-1]{compound-key-n}
```

`id`\</a\>"\>Example paths:

``` http
/shopping-carts/{country}/{session-id}
/shopping-carts/{country}/{session-id}/items/{item-id}
/api-specifications/{docker-image-id}/apis/{path}/{file-name}
/api-specifications/{repository-name}/{artifact-name}:{tag}
/article-size-advices/{sku}/{sales-channel}
```

`id`\</a\>"\>**Warning:** Exposing a compound key as described above
limits ability to evolve the structure of the resource identifier as it
is no longer opaque.

`id`\</a\>"\>To compensate for this drawback, APIs must apply a compound
key abstraction consistently in all requests and responses parameters
and attributes allowing consumers to treat these as *technical resource
identifier* replacement. The use of independent compound key components
must be limited to search and creation requests, as follows:

``` http
# compound key components passed as independent search query parameters
GET /article-size-advices?skus=sku-1,sku-2&sales_channel_id=sid-1
=> { "items": [{ "id": "id-1", ...  },{ "id": "id-2", ...  }] }

# opaque technical resource identifier passed as path parameter
GET /article-size-advices/id-1
=> { "id": "id-1", "sku": "sku-1", "sales_channel_id": "sid-1", "size": ... }

# compound key components passed as mandatory request fields
POST /article-size-advices { "sku": "sku-1", "sales_channel_id": "sid-1", "size": ... }
=> { "id": "id-1", "sku": "sku-1", "sales_channel_id": "sid-1", "size": ... }
```

`id`\</a\>"\>Where `id-1` is representing the opaque provision of the
compound key `sku-1/sid-1` as technical resource identifier.

`id`\</a\>"\>**Remark:** A compound key component may itself be used as
another resource identifier providing another resource endpoint, e.g
`/article-size-advices/{sku}`.

`id`\</a\>"\>If a sub-resource is only accessible via its parent
resource and may not exist without parent resource, consider using a
nested URL structure, for instance:

``` http
/shoping-carts/de/1681e6b88ec1/cart-items/1
```

`id`\</a\>"\>However, if the resource can be accessed directly via its
unique id, then the API should expose it as a top-level resource. For
example, customer has a collection for sales orders; however, sales
orders have globally unique id and some services may choose to access
the orders directly, for instance:

``` http
/customers/1637asikzec1
/sales-orders/5273gh3k525a
```

`id`\</a\>"\>Generating IDs can be a scaling problem in high frequency
and near real time use cases. UUIDs solve this problem, as they can be
generated without collisions in a distributed, non-coordinated way and
without additional server round trips.

`id`\</a\>"\>However, they also come with some disadvantages:

  - pure technical key without meaning; not ready for naming or name
    scope conventions that might be helpful for pragmatic reasons, e.g.
    we learned to use names for product attributes, instead of UUIDs

  - less usable, because…

  - cannot be memorized and easily communicated by humans

  - harder to use in debugging and logging analysis

  - less convenient for consumer facing usage

  - quite long: readable representation requires 36 characters and comes
    with higher memory and bandwidth consumption

  - not ordered along their creation history and no indication of used
    id volume

  - may be in conflict with additional backward compatibility support of
    legacy ids

`id`\</a\>"\>UUIDs should be avoided when not needed for large scale id
generation. Instead, for instance, server side support with id
generation can be preferred (`POST` on id resource, followed by
idempotent `PUT` on entity resource). Usage of UUIDs is especially
discouraged as primary keys of master and configuration data, like
brand-ids or attribute-ids which have low id volume but widespread
steering functionality.

`id`\</a\>"\>Please be aware that sequential, strictly monotonically
increasing numeric identifiers may reveal critical, confidential
business information, like order volume, to non-privileged clients.

`id`\</a\>"\>In any case, we should always use string rather than number
type for identifiers. This gives us more flexibility to evolve the
identifier naming scheme. Accordingly, if used as identifiers, UUIDs
should not be qualified using a format property.

`id`\</a\>"\>Hint: Usually, random UUID is used - see UUID version 4 in
[RFC 4122](https://tools.ietf.org/html/rfc4122). Though UUID version 1
also contains leading timestamps it is not reflected by its
lexicographic sorting. This deficit is addressed by
[ULID](https://github.com/alizain/ulid) (Universally Unique
Lexicographically Sortable Identifier). You may favour ULID instead of
UUID, for instance, for pagination use cases ordered along creation
time.

`id`\</a\>"\>To keep maintenance and service evolution manageable, we
should follow "functional segmentation" and "separation of concern"
design principles and do not mix different business functionalities in
same API definition. In practice this means that the number of resource
types exposed via an API should be limited. In this context a resource
type is defined as a set of highly related resources such as a
collection, its members and any direct sub-resources.

`id`\</a\>"\>For example, the resources below would be counted as three
resource types, one for customers, one for the addresses, and one for
the customers' related addresses:

``` http
/customers
/customers/{id}
/customers/{id}/preferences
/customers/{id}/addresses
/customers/{id}/addresses/{addr}
/addresses
/addresses/{addr}
```

`id`\</a\>"\>Note that:

  - We consider `/customers/{id}/preferences` part of the `/customers`
    resource type because it has a one-to-one relation to the customer
    without an additional identifier.

  - We consider `/customers` and `/customers/{id}/addresses` as separate
    resource types because `/customers/{id}/addresses/{addr}` also
    exists with an additional identifier for the address.

  - We consider `/addresses` and `/customers/{id}/addresses` as separate
    resource types because there’s no reliable way to be sure they are
    the same.

`id`\</a\>"\>Given this definition, our experience is that well defined
APIs involve no more than 4 to 8 resource types. There may be exceptions
with more complex business domains that require more resources, but you
should first check if you can split them into separate subdomains with
distinct APIs.

`id`\</a\>"\>Nevertheless one API should hold all necessary resources to
model complete business processes helping clients to understand these
flows.

`id`\</a\>"\>There are main resources (with root url paths) and
sub-resources (or *nested* resources with non-root urls paths). Use
sub-resources if their life cycle is (loosely) coupled to the main
resource, i.e. the main resource works as collection resource of the
subresource entities. You should use ⇐ 3 sub-resource (nesting)
levels — more levels increase API complexity and url path length.
(Remember, some popular web browsers do not support URLs of more than
2000 characters.)

# HTTP requests and responses

`id`\</a\>"\>Be compliant with the standardized HTTP method semantics
summarized as follows:

## GET

`id`\</a\>"\>`GET` requests are used to **read** either a single or a
collection resource.

  - `GET` requests for individual resources will usually generate a 404
    if the resource does not exist

  - `GET` requests for collection resources may return either 200 (if
    the collection is empty) or 404 (if the collection is missing)

  - `GET` requests must NOT have a request body payload (see `GET with
    body`)

`id`\</a\>"\>**Note:** `GET` requests on collection resources should
provide sufficient [filter](#137) and [Pagination](#pagination)
mechanisms.

## GET with body payload

`id`\</a\>"\>APIs sometimes face the problem, that they have to provide
extensive structured request information with `GET`, that may conflict
with the size limits of clients, load-balancers, and servers. As we
require APIs to be standard conform (request body payload in `GET` must
be ignored on server side), API designers have to check the following
two options:

1.  `GET` with URL encoded query parameters: when it is possible to
    encode the request information in query parameters, respecting the
    usual size limits of clients, gateways, and servers, this should be
    the first choice. The request information can either be provided via
    multiple query parameters or by a single structured URL encoded
    string.

2.  `POST` with body payload content: when a `GET` with URL encoded
    query parameters is not possible, a `POST` request with body payload
    must be used, and explicitly documented with a hint like in the
    following example:

<!-- end list -->

``` yaml
paths:
  /products/productsSearch:
    post:
      description: >
        No resources created:
        Returns all products matching the query passed as request input payload.
      requestBody:
        required: true
        content:
          ...
```

`id`\</a\>"\>**Note:** It is no option to encode the lengthy structured
request information using header parameters. From a conceptual point of
view, the semantic of an operation should always be expressed by the
resource names, as well as the involved path and query parameters. In
other words by everything that goes into the URL. Request headers are
reserved for general context information (see [???](#183)). In addition,
size limits on query parameters and headers are not reliable and depend
on clients, gateways, server, and actual settings. Thus, switching to
headers does not solve the original problem.

`id`\</a\>"\>**Hint:** As `GET with body` is used to transport extensive
query parameters, the `cursor` cannot any longer be used to encode the
query filters in case of [cursor-based pagination](#160). As a
consequence, it is best practice to transport the query filters in the
body payload, while using [pagination links](#161) containing the
`cursor` that is only encoding the page position and direction. To
protect the pagination sequence the `cursor` may contain a hash over all
applied query filters (See also [???](#161)).

## PUT

`id`\</a\>"\>`PUT` requests are used to **update** (and sometimes to
create) **entire** resources – single or collection resources. The
semantic is best described as *"please put the enclosed representation
at the resource mentioned by the URL, replacing any existing
resource."*.

  - `PUT` requests are usually applied to single resources, and not to
    collection resources, as this would imply replacing the entire
    collection

  - `PUT` requests are usually robust against non-existence of resources
    by implicitly creating the resource before updating

  - on successful `PUT` requests, the server will **replace the entire
    resource** addressed by the URL with the representation passed in
    the payload (subsequent reads will deliver the same payload)

  - successful `PUT` requests will usually generate 200 or 204 (if the
    resource was updated – with or without actual content returned), and
    201 (if the resource was created)

`id`\</a\>"\>**Important:** It is good practice to prefer `POST` over
`PUT` for creation of (at least top-level) resources. This leaves the
resource ID management under control of the service and not the client,
and focus `PUT` on its usage for updates. However, in situations where
`PUT` is used for resource creation, the resource IDs are maintained by
the client and passed as a URL path segment. Putting the same resource
twice is required to be [idempotent](#idempotent) and to result in the
same single resource instance (see [???](#149)).

`id`\</a\>"\>**Hint:** To prevent unnoticed concurrent updates and
duplicate creations when using `PUT`, you [???](#182) to allow the
server to react on stricter demands that expose conflicts and prevent
lost updates. See also [Optimistic locking in RESTful
APIs](#optimistic-locking) for details and options.

## POST

`id`\</a\>"\>`POST` requests are idiomatically used to **create** single
resources on a collection resource endpoint, but other semantics on
single resources endpoint are equally possible. The semantic for
collection endpoints is best described as *"please add the enclosed
representation to the collection resource identified by the URL"*. The
semantic for single resource endpoints is best described as *"please
execute the given well specified request on the resource identified by
the URL"*.

  - on a successful `POST` request, the server will create one or
    multiple new resources and provide their URI/URLs in the response

  - successful `POST` requests will usually generate 200 (if resources
    have been updated), 201 (if resources have been created), 202 (if
    the request was accepted but has not been finished yet), and
    exceptionally 204 with `Location` header (if the actual resource is
    not returned).

`id`\</a\>"\>**Note:** By using `POST` to create resources the resource
ID must not be passed as request input data by the client, but created
and maintained by the service and returned with the response payload.

`id`\</a\>"\>Apart from resource creation, `POST` should be also used
for scenarios that cannot be covered by the other methods sufficiently.
However, in such cases make sure to document the fact that `POST` is
used as a workaround (see e.g. `GET with body`).

`id`\</a\>"\>**Hint:** Posting the same resource twice is **not**
required to be [idempotent](#idempotent) (check [???](#149)) and may
result in multiple resources. However, you [???](#229) to prevent this.

## PATCH

`id`\</a\>"\>`PATCH` requests are used to **update parts** of single
resources, i.e. where only a specific subset of resource fields should
be replaced. The semantic is best described as *"please change the
resource identified by the URL according to my change request"*. The
semantic of the change request is not defined in the HTTP standard and
must be described in the API specification by using suitable media
types.

  - `PATCH` requests are usually applied to single resources as patching
    entire collection is challenging

  - `PATCH` requests are usually not robust against non-existence of
    resource instances

  - on successful `PATCH` requests, the server will update parts of the
    resource addressed by the URL as defined by the change request in
    the payload

  - successful `PATCH` requests will usually generate 200 or 204 (if
    resources have been updated with or without updated content
    returned)

`id`\</a\>"\>**Note:** since implementing `PATCH` correctly is a bit
tricky, we strongly suggest to choose one and only one of the following
patterns per endpoint, unless forced by a [backwards compatible
change](#106). In preference order:

1.  use `PUT` with complete objects to update a resource as long as
    feasible (i.e. do not use `PATCH` at all).

2.  use `PATCH` with partial objects to only update parts of a resource,
    whenever possible. (This is basically [JSON Merge
    Patch](https://tools.ietf.org/html/rfc7396), a specialized media
    type `application/merge-patch+json` that is a partial resource
    representation.)

3.  use `PATCH` with [JSON Patch](https://tools.ietf.org/html/rfc6902),
    a specialized media type `application/json-patch+json` that includes
    instructions on how to change the resource.

4.  use `POST` (with a proper description of what is happening) instead
    of `PATCH`, if the request does not modify the resource in a way
    defined by the semantics of the media type.

`id`\</a\>"\>In practice [JSON Merge
Patch](https://tools.ietf.org/html/rfc7396) quickly turns out to be too
limited, especially when trying to update single objects in large
collections (as part of the resource). In these cases [JSON
Patch](https://tools.ietf.org/html/rfc6902) can show its full power
while still showing readable patch requests (see also [JSON patch vs.
merge](http://erosb.github.io/post/json-patch-vs-merge-patch)).

`id`\</a\>"\>**Note:** Patching the same resource twice is **not**
required to be [idempotent](#idempotent) (check [???](#149)) and may
result in a changing result. However, you [???](#229) to prevent this.

`id`\</a\>"\>**Hint:** To prevent unnoticed concurrent updates when
using `PATCH` you [???](#182) to allow the server to react on stricter
demands that expose conflicts and prevent lost updates. See [Optimistic
locking in RESTful APIs](#optimistic-locking) and [???](#229) for
details and options.

`id`\</a\>"\>`DELETE` requests are used to **delete** resources. The
semantic is best described as *"please delete the resource identified by
the URL"*.

  - `DELETE` requests are usually applied to single resources, not on
    collection resources, as this would imply deleting the entire
    collection.

  - `DELETE` request can be applied to multiple resources at once using
    query parameters on the collection resource (see [DELETE with query
    parameters](#delete-with-query-params)).

  - successful `DELETE` requests will usually generate 200 (if the
    deleted resource is returned) or 204 (if no content is returned).

  - failed `DELETE` requests will usually generate 404 (if the resource
    cannot be found) or 410 (if the resource was already deleted
    before).

`id`\</a\>"\>**Important:** After deleting a resource with `DELETE`, a
`GET` request on the resource is expected to either return 404 (not
found) or 410 (gone) depending on how the resource is represented after
deletion. Under no circumstances the resource must be accessible after
this operation on its endpoint.

## DELETE with query parameters

`id`\</a\>"\>`DELETE` request can have query parameters. Query
parameters should be used as filter parameters on a resource and not for
passing context information to control the operation behavior.

``` http
DELETE /resources?param1=value1&param2=value2...&paramN=valueN
```

`id`\</a\>"\>**Note:** When providing `DELETE` with query parameters,
API designers must carefully document the behavior in case of (partial)
failures to manage client expectations properly.

`id`\</a\>"\>The response status code of `DELETE` with query parameters
requests should be similar to usual `DELETE` requests. In addition, it
may return the status code 207 using a payload describing the operation
results (see [???](#152) for details).

## DELETE with body payload

`id`\</a\>"\>In rare cases `DELETE` may require additional information,
that cannot be classified as filter parameters and thus should be
transported via request body payload, to perform the operation. Since
[RFC-7231](https://tools.ietf.org/html/rfc7231#section-4.3.5) states,
that `DELETE` has an undefined semantic for payloads, we recommend to
utilize `POST`. In this case the POST endpoint must be documented with
the hint `DELETE with body` analog to how it is defined for `GET with
body`. The response status code of `DELETE with body` requests should be
similar to usual `DELETE` requests.

## HEAD

`id`\</a\>"\>`HEAD` requests are used to **retrieve** the header
information of single resources and resource collections.

  - `HEAD` has exactly the same semantics as `GET`, but returns headers
    only, no body.

`id`\</a\>"\>**Hint:** `HEAD` is particular useful to efficiently lookup
whether large resources or collection resources have been updated in
conjunction with the `ETag`-header.

## OPTIONS

`id`\</a\>"\>`OPTIONS` requests are used to **inspect** the available
operations (HTTP methods) of a given endpoint.

  - `OPTIONS` responses usually either return a comma separated list of
    methods in the `Allow` header or as a structured list of link
    templates

`id`\</a\>"\>**Note:** `OPTIONS` is rarely implemented, though it could
be used to self-describe the full functionality of a resource.

`id`\</a\>"\>Request methods in RESTful services can be…

  - safe - the operation semantic is defined to be read-only, meaning it
    must not have *intended side effects*, i.e. changes, to the server
    state.

  - idempotent - the operation has the same *intended effect* on the
    server state, independently whether it is executed once or multiple
    times. **Note:** this does not require that the operation is
    returning the same response or status code.

  - cacheable - to indicate that responses are allowed to be stored for
    future reuse. In general, requests to safe methods are cachable, if
    it does not require a current or authoritative response from the
    server.

`id`\</a\>"\>**Note:** The above definitions, of *intended (side)
effect* allows the server to provide additional state changing behavior
as logging, accounting, pre- fetching, etc. However, these actual
effects and state changes, must not be intended by the operation so that
it can be held accountable.

`id`\</a\>"\>Method implementations must fulfill the following basic
properties according to [RFC 7231](https://tools.ietf.org/html/rfc7231):

| Method    | Safe  | Idempotent             | Cacheable                                                                                              |
| --------- | ----- | ---------------------- | ------------------------------------------------------------------------------------------------------ |
| `GET`     | ✔ Yes | ✔ Yes                  | ✔ Yes                                                                                                  |
| `HEAD`    | ✔ Yes | ✔ Yes                  | ✔ Yes                                                                                                  |
| `POST`    | ✗ No  | ⚠️ No, but [???](#229) | ⚠️ May, but only if specific `POST` endpoint is [safe](#safe). **Hint:** not supported by most caches. |
| `PUT`     | ✗ No  | ✔ Yes                  | ✗ No                                                                                                   |
| `PATCH`   | ✗ No  | ⚠️ No, but [???](#229) | ✗ No                                                                                                   |
| `DELETE`  | ✗ No  | ✔ Yes                  | ✗ No                                                                                                   |
| `OPTIONS` | ✔ Yes | ✔ Yes                  | ✗ No                                                                                                   |
| `TRACE`   | ✔ Yes | ✔ Yes                  | ✗ No                                                                                                   |

`id`\</a\>"\>**Note:** [???](#227).

`id`\</a\>"\>In many cases it is helpful or even necessary to design
`POST` and `PATCH` [idempotent](#idempotent) for clients to expose
conflicts and prevent resource duplicate (a.k.a. zombie resources) or
lost updates, e.g. if same resources may be created or changed in
parallel or multiple times. To design an [idempotent](#idempotent) API
endpoint owners should consider to apply one of the following three
patterns.

  - A resource specific **conditional key** provided via [`If-Match`
    header](#182) in the request. The key is in general a meta
    information of the resource, e.g. a *hash* or *version number*,
    often stored with it. It allows to detect concurrent creations and
    updates to ensure [idempotent](#idempotent) behavior (see
    [???](#182)).

  - A resource specific **secondary key** provided as resource property
    in the request body. The *secondary key* is stored permanently in
    the resource. It allows to ensure [idempotent](#idempotent) behavior
    by looking up the unique secondary key in case of multiple
    independent resource creations from different clients (see
    [???](#231)).

  - A client specific **idempotency key** provided via `Idempotency-Key`
    header in the request. The key is not part of the resource but
    stored temporarily pointing to the original response to ensure
    [idempotent](#idempotent) behavior when retrying a request (see
    [???](#230)).

`id`\</a\>"\>**Note:** While **conditional key** and **secondary key**
are focused on handling concurrent requests, the **idempotency key** is
focused on providing the exact same responses, which is even a
*stronger* requirement than the [idempotency defined
above](#idempotent). It can be combined with the two other patterns.

`id`\</a\>"\>To decide, which pattern is suitable for your use case,
please consult the following table showing the major properties of each
pattern:

|                                       |                 |               |                 |
| ------------------------------------- | --------------- | ------------- | --------------- |
|                                       | Conditional Key | Secondary Key | Idempotency Key |
| Applicable with                       | `PATCH`         | `POST`        | `POST`/`PATCH`  |
| HTTP Standard                         | ✔ Yes           | ✗ No          | ✗ No            |
| Prevents duplicate (zombie) resources | ✔ Yes           | ✔ Yes         | ✗ No            |
| Prevents concurrent lost updates      | ✔ Yes           | ✗ No          | ✗ No            |
| Supports safe retries                 | ✔ Yes           | ✔ Yes         | ✔ Yes           |
| Supports exact same response          | ✗ No            | ✗ No          | ✔ Yes           |
| Can be inspected (by intermediaries)  | ✔ Yes           | ✗ No          | ✔ Yes           |
| Usable without previous `GET`         | ✗ No            | ✔ Yes         | ✔ Yes           |

`id`\</a\>"\>**Note:** The patterns applicable to `PATCH` can be applied
in the same way to `PUT` and `DELETE` providing the same properties.

`id`\</a\>"\>If you mainly aim to support safe retries, we suggest to
apply [conditional key](#182) and [secondary key](#231) pattern before
the [Idempotency Key](#230) pattern.

`id`\</a\>"\>The most important pattern to design `POST`
[idempotent](#idempotent) for creation is to introduce a resource
specific **secondary key** provided in the request body, to eliminate
the problem of duplicate (a.k.a zombie) resources.

`id`\</a\>"\>The secondary key is stored permanently in the resource as
*alternate key* or *combined key* (if consisting of multiple properties)
guarded by a uniqueness constraint enforced server-side, that is visible
when reading the resource. The best and often naturally existing
candidate is a *unique foreign key*, that points to another resource
having *one-on-one* relationship with the newly created resource, e.g. a
parent process identifier.

`id`\</a\>"\>A good example here for a secondary key is the shopping
cart ID in an order resource.

`id`\</a\>"\>**Note:** When using the secondary key pattern without
`Idempotency-Key` all subsequent retries should fail with status code
409 (conflict). We suggest to avoid 200 here unless you make sure, that
the delivered resource is the original one implementing a well defined
behavior. Using 204 without content would be a similar well defined
option.

`id`\</a\>"\>Header and query parameters allow to provide a collection
of values, either by providing a comma-separated list of values or by
repeating the parameter multiple times with different values as follows:

|                |                         |                                  |                                                                             |
| -------------- | ----------------------- | -------------------------------- | --------------------------------------------------------------------------- |
| Parameter Type | Comma-separated Values  | Multiple Parameters              | Standard                                                                    |
| Header         | `Header: value1,value2` | `Header: value1, Header: value2` | [RFC 7230 Section 3.2.2](https://tools.ietf.org/html/rfc7230#section-3.2.2) |
| Query          | `?param=value1,value2`  | `?param=value1&param=value2`     | [RFC 6570 Section 3.2.8](https://tools.ietf.org/html/rfc6570#section-3.2.8) |

`id`\</a\>"\>As Open API does not support both schemas at once, an API
specification must explicitly define the collection format to guide
consumers as follows:

|                |                                 |                                                                                               |
| -------------- | ------------------------------- | --------------------------------------------------------------------------------------------- |
| Parameter Type | Comma-separated Values          | Multiple Parameters                                                                           |
| Header         | `style: simple, explode: false` | not allowed (see [RFC 7230 Section 3.2.2](https://tools.ietf.org/html/rfc7230#section-3.2.2)) |
| Query          | `style: form, explode: false`   | `style: form, explode: true`                                                                  |

`id`\</a\>"\>When choosing the collection format, take into account the
tool support, the escaping of special characters and the maximal URL
length.

`id`\</a\>"\>We prefer the use of query parameters to describe
resource-specific query languages for the majority of APIs because it’s
native to HTTP, easy to extend and has excellent implementation support
in HTTP clients and web frameworks.

`id`\</a\>"\>Query parameters should have the following aspects
specified:

  - Reference to corresponding property, if any

  - Value range, e.g. inclusive vs. exclusive

  - Comparison semantics (equals, less than, greater than, etc)

  - Implications when combined with other queries, e.g. *and* vs. *or*

`id`\</a\>"\>How query parameters are named and used is up to individual
API designers. The following examples should serve as ideas:

  - `name=Bit`, to query for elements based on property equality

  - `age=5`, to query for elements based on logical properties
    
      - Assuming that elements don’t actually have an `age` but rather a
        `birthday`

  - `max_length=5`, based on upper and lower bounds (`min` and `max`)

  - `shorter_than=5`, using terminology specific e.g. to *length*

  - `created_before=2019-07-17` or `not_modified_since=2019-07-17`
    
      - Using terminology specific e.g. to time: *before*, *after*,
        *since* and *until*

`id`\</a\>"\>We don’t advocate for or against certain names because in
the end APIs should be free to choose the terminology that fits their
domain the best.

`id`\</a\>"\>Minimalistic query languages based on [query
parameters](#236) are suitable for simple use cases with a small set of
available filters that are combined in one way and one way only (e.g.
*and* semantics). Simple query languages are generally preferred over
complex ones.

`id`\</a\>"\>Some APIs will have a need for sophisticated and more
complex query languages. Dominant examples are APIs around search (incl.
faceting) and product catalogs.

`id`\</a\>"\>Aspects that set those APIs apart from the rest include but
are not limited to:

  - Unusual high number of available filters

  - Dynamic filters, due to a dynamic and extensible resource model

  - Free choice of operators, e.g. `and`, `or` and `not`

`id`\</a\>"\>APIs that qualify for a specific, complex query language
are encouraged to use nested JSON data structures and define them using
Open API directly. This provides the following benefits:

  - Data structures are easy to use for clients
    
      - No special library support necessary
    
      - No need for string concatenation or manual escaping

  - Data structures are easy to use for servers
    
      - No special tokenizers needed
    
      - Semantics are attached to data structures rather than text
        tokens

  - Consistent with other HTTP methods

  - API is defined in Open API completely
    
      - No external documents or grammars needed
    
      - Existing means are familiar to everyone

`id`\</a\>"\>[JSON-specific rules](#json-guidelines) and most certainly
needs to make use of the [`GET`-with-body](#get-with-body) pattern.

## Example

`id`\</a\>"\>The following JSON document should serve as an idea how a
structured query might look like.

``` json
{
  "and": {
    "name": {
      "match": "Alice"
    },
    "age": {
      "or": {
        "range": {
          ">": 25,
          "<=": 50
        },
        "=": 65
      }
    }
  }
}
```

`id`\</a\>"\>Feel free to also get some inspiration from:

  - [Elastic Search: Query
    DSL](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)

  - [GraphQL: Queries](https://graphql.org/learn/queries/)

`id`\</a\>"\>Sometimes certain collection resources or queries will not
list all the possible elements they have, but only those for which the
current client is authorized to access.

`id`\</a\>"\>Implicit filtering could be done on:

  - the collection of resources being returned on a `GET` request

  - the fields returned for the detail information of the resource

`id`\</a\>"\>In such cases, the fact that implicit filtering is applied
must be documented in the API specification’s endpoint description.
Consider [caching aspects](#227) when implicit filtering is provided.
Example:

`id`\</a\>"\>If an employee of the company *Foo* accesses one of our
business-to-business service and performs a `{GET} /business-partners`,
it must, for legal reasons, not display any other business partner that
is not owned or contractually managed by her/his company. It should
never see that we are doing business also with company *Bar*.

`id`\</a\>"\>Response as seen from a consumer working at `FOO`:

``` json
{
    "items": [
        { "name": "Foo Performance" },
        { "name": "Foo Sport" },
        { "name": "Foo Signature" }
    ]
}
```

`id`\</a\>"\>Response as seen from a consumer working at `BAR`:

``` json
{
    "items": [
        { "name": "Bar Classics" },
        { "name": "Bar pour Elle" }
    ]
}
```

`id`\</a\>"\>The API Specification should then specify something like
this:

``` yaml
paths:
  /business-partner:
    get:
      description: >-
        Get the list of registered business partner.
        Only the business partners to which you have access to are returned.
```

# HTTP status codes and errors

`id`\</a\>"\>APIs should define the functional, business view and
abstract from implementation aspects. Success and error responses are a
vital part to define how an API is used correctly.

`id`\</a\>"\>Therefore, you must define **all** success and service
specific error responses in your API specification. Both are part of the
interface definition and provide important information for service
clients to handle standard as well as exceptional situations.

`id`\</a\>"\>**Hint:** In most cases it is not useful to document all
technical errors, especially if they are not under control of the
service provider. Thus unless a response code conveys
application-specific functional semantics or is used in a none standard
way that requires additional explanation, multiple error response
specifications can be combined using the following pattern (see also
\<\<\#234\>\>):

``` yaml
responses:
  ...
  default:
    description: error occurred - see status code and problem object for more information.
    content:
      "application/problem+json":
        schema:
          $ref: 'https://github.com/sonaemc/api-guidelines/problem-1.0.1.yaml#/Problem'
```

`id`\</a\>"\>API designers should also think about a **troubleshooting
board** as part of the associated online API documentation. It provides
information and handling guidance on application-specific errors and is
referenced via links from the API specification. This can reduce service
support tasks and contribute to service client and provider performance.

`id`\</a\>"\>You must only use standardized HTTP status codes
consistently with their intended semantics. You must not invent new HTTP
status codes.

`id`\</a\>"\>RFC standards define \~60 different HTTP status codes with
specific semantics (mainly
[RFC7231](https://tools.ietf.org/html/rfc7231#section-6) and
[RFC 6585](https://tools.ietf.org/html/rfc6585)) — and there are
upcoming new ones, e.g. [draft
legally-restricted-status](https://tools.ietf.org/html/draft-tbray-http-legally-restricted-status-05).
See overview on all error codes on
[Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) or
via <https://httpstatuses.com/> also including *unofficial codes*, e.g.
used by popular web servers like Nginx.

`id`\</a\>"\>Below we list the most commonly used and best understood
HTTP status codes, consistent with their semantic in the RFCs. APIs
should only use these to prevent misconceptions that arise from less
commonly used HTTP status codes.

`id`\</a\>"\>**Important:** As long as your HTTP status code usage is
well covered by the semantic defined here, you should not describe it to
avoid an overload with common sense information and the risk of
inconsistent definitions. Only if the HTTP status code is not in the
list below or its usage requires additional information aside the well
defined semantic, the API specification must provide a clear description
of the HTTP status code in the response.

## Success codes

| Code | Meaning                                                                                                                                                                                                                                                  | Methods                          |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 200  | OK - this is the standard success response                                                                                                                                                                                                               | `<all>`                          |
| 201  | Created - Returned on successful entity creation. You are free to return either an empty response or the created resource in conjunction with the Location header. (More details found in the [???](#common-headers).) *Always* set the Location header. | `POST`, `PUT`                    |
| 202  | Accepted - The request was successful and will be processed asynchronously.                                                                                                                                                                              | `POST`, `PUT`, `PATCH`, `DELETE` |
| 204  | No content - There is no response body.                                                                                                                                                                                                                  | `PUT`, `PATCH`, `DELETE`         |
| 207  | Multi-Status - The response body contains multiple status informations for different parts of a batch/bulk request (see [???](#152)).                                                                                                                    | `POST`, (`DELETE`)               |

## Redirection codes

| Code | Meaning                                                                                                                                                                                                                                                                                             | Methods                          |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 301  | Moved Permanently - This and all future requests should be directed to the given URI.                                                                                                                                                                                                               | `<all>`                          |
| 303  | See Other - The response to the request can be found under another URI using a `GET` method.                                                                                                                                                                                                        | `POST`, `PUT`, `PATCH`, `DELETE` |
| 304  | Not Modified - indicates that a conditional GET or HEAD request would have resulted in 200 response if it were not for the fact that the condition evaluated to false, i.e. resource has not been modified since the date or version passed via request headers If-Modified-Since or If-None-Match. | `GET`, `HEAD`                    |

## Client side error codes

| Code | Meaning                                                                                                                                                        | Methods                          |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 400  | Bad request - generic / unknown error. Should also be delivered in case of input payload fails business logic validation.                                      | `<all>`                          |
| 401  | Unauthorized - the users must log in (this often means "Unauthenticated").                                                                                     | `<all>`                          |
| 403  | Forbidden - the user is not authorized to use this resource.                                                                                                   | `<all>`                          |
| 404  | Not found - the resource is not found.                                                                                                                         | `<all>`                          |
| 405  | Method Not Allowed - the method is not supported, see `OPTIONS`.                                                                                               | `<all>`                          |
| 406  | Not Acceptable - resource can only generate content not acceptable according to the Accept headers sent in the request.                                        | `<all>`                          |
| 408  | Request timeout - the server times out waiting for the resource.                                                                                               | `<all>`                          |
| 409  | Conflict - request cannot be completed due to conflict, e.g. when two clients try to create the same resource or if there are concurrent, conflicting updates. | `POST`, `PUT`, `PATCH`, `DELETE` |
| 410  | Gone - resource does not exist any longer, e.g. when accessing a resource that has intentionally been deleted.                                                 | `<all>`                          |
| 412  | Precondition Failed - returned for conditional requests, e.g. `If-Match` if the condition failed. Used for optimistic locking.                                 | `PUT`, `PATCH`, `DELETE`         |
| 415  | Unsupported Media Type - e.g. clients sends request body without content type.                                                                                 | `POST`, `PUT`, `PATCH`, `DELETE` |
| 423  | Locked - Pessimistic locking, e.g. processing states.                                                                                                          | `PUT`, `PATCH`, `DELETE`         |
| 428  | Precondition Required - server requires the request to be conditional, e.g. to make sure that the "lost update problem" is avoided (see [???](#181)).          | `<all>`                          |
| 429  | Too many requests - the client does not consider rate limiting and sent too many requests (see [???](#153)).                                                   | `<all>`                          |

## Server side error codes:

| Code | Meaning                                                                                                                                                                                                                                                                          | Methods |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| 500  | Internal Server Error - a generic error indication for an unexpected server execution problem (here, client retry may be sensible)                                                                                                                                               | `<all>` |
| 501  | Not Implemented - server cannot fulfill the request (usually implies future availability, e.g. new feature).                                                                                                                                                                     | `<all>` |
| 503  | Service Unavailable - service is (temporarily) not available (e.g. if a required component or downstream service is not available) — client retry may be sensible. If possible, the service should indicate how long the client should wait by setting the `Retry-After` header. | `<all>` |

`id`\</a\>"\>You must use the most specific HTTP status code when
returning information about your request processing status or error
situations.

`id`\</a\>"\>Some APIs are required to provide either *batch* or *bulk*
requests using `POST` for performance reasons, i.e. for communication
and processing efficiency. In this case services may be in need to
signal multiple response codes for each part of a batch or bulk request.
As HTTP does not provide proper guidance for handling batch/bulk
requests and responses, we herewith define the following approach:

  - A batch or bulk request **always** responds with HTTP status code
    207 unless a non-item-specific failure occurs.

  - A batch or bulk request **may** return 4xx/5xx status codes, if the
    failure is non-item-specific and cannot be restricted to individual
    items of the batch or bulk request, e.g. in case of overload
    situations or general service failures.

  - A batch or bulk response with status code 207 **always** returns as
    payload a multi-status response containing item specific status
    and/or monitoring information for each part of the batch or bulk
    request.

`id`\</a\>"\>**Note:** These rules apply *even in the case* that
processing of all individual parts *fail* or each part is executed
*asynchronously*\!

`id`\</a\>"\>The rules are intended to allow clients to act on batch and
bulk responses in a consistent way by inspecting the individual results.
We explicitly reject the option to apply 200 for a completely successful
batch as proposed in Nakadi’s [`POST
/event-types/{name}/events`](https://nakadi.io/manual.html#/event-types/name/events_post)
as short cut without inspecting the result, as we want to avoid risks
and expect clients to handle partial batch failures anyway.

`id`\</a\>"\>The bulk or batch response may look as follows:

``` yaml
BatchOrBulkResponse:
  description: batch response object.
  type: object
  properties:
    items:
      type: array
      items:
        type: object
        properties:
          id:
            description: Identifier of batch or bulk request item.
            type: string
          status:
            description: >
              Response status value. A number or extensible enum describing
              the execution status of the batch or bulk request items.
            type: string
            x-extensible-enum: [...]
          description:
            description: >
              Human readable status description and containing additional
              context information about failures etc.
            type: string
        required: [id, status]
```

`id`\</a\>"\>**Note**: while a *batch* defines a collection of requests
triggering independent processes, a *bulk* defines a collection of
independent resources created or updated together in one request. With
respect to response processing this distinction normally does not
matter.

`id`\</a\>"\>APIs that wish to manage the request rate of clients must
use the 429 (Too Many Requests) response code, if the client exceeded
the request rate (see [RFC 6585](https://tools.ietf.org/html/rfc6585)).
Such responses must also contain header information providing further
details to the client. There are two approaches a service can take for
header information:

  - Return a `Retry-After` header indicating how long the client ought
    to wait before making a follow-up request. The Retry-After header
    can contain a HTTP date value to retry after or the number of
    seconds to delay. Either is acceptable but APIs should prefer to use
    a delay in seconds.

  - Return a trio of `X-RateLimit` headers. These headers (described
    below) allow a server to express a service level in the form of a
    number of allowing requests within a given window of time and when
    the window is reset.

`id`\</a\>"\>The `X-RateLimit` headers are:

  - `X-RateLimit-Limit`: The maximum number of requests that the client
    is allowed to make in this window.

  - `X-RateLimit-Remaining`: The number of requests allowed in the
    current window.

  - `X-RateLimit-Reset`: The relative time in seconds when the rate
    limit window will be reset. **Beware** that this is different to
    Github and Twitter’s usage of a header with the same name which is
    using UTC epoch seconds instead.

`id`\</a\>"\>The reason to allow both approaches is that APIs can have
different needs. Retry-After is often sufficient for general load
handling and request throttling scenarios and notably, does not strictly
require the concept of a calling entity such as a tenant or named
account. In turn this allows resource owners to minimise the amount of
state they have to carry with respect to client requests. The
*X-RateLimit* headers are suitable for scenarios where clients are
associated with pre-existing account or tenancy structures.
*X-RateLimit* headers are generally returned on every request and not
just on a 429, which implies the service implementing the API is
carrying sufficient state to track the number of requests made within a
given window for each named entity.

`id`\</a\>"\>[RFC 7807](https://tools.ietf.org/html/rfc7807) defines a
Problem JSON object using the media type `application/problem+json` to
provide an extensible human and machine readable failure information
beyond the HTTP response status code to transport the failure kind
(`type` / `title`) and the failure cause and location (`instant` /
`detail`). To make best use of this additional failure information,
every endpoint must be capable of returning a Problem JSON on client
usage errors (4xx status codes) as well as server side processing errors
(5xx status codes).

`id`\</a\>"\>**Note:** Clients must be robust and **not rely** on a
Problem JSON object being returned, since (a) failure responses may be
created by infrastructure components not aware of this guideline or (b)
service may be unable to comply with this guidelines in certain error
situations.

`id`\</a\>"\>**Hint:** The media type `application/problem+json` is
often not implemented as a subset of `application/json` by libraries and
services\! Thus clients need to include `application/problem+json` in
the `Accept`-Header to trigger delivery of the extended failure
information.

`id`\</a\>"\>The Open API schema definition of the Problem JSON object
can be found [on
GitHub](https://github.com/sonaemc/api-guidelines/blob/main/models/problem-1.0.1.yaml).
You can reference it by using:

``` yaml
responses:
  503:
    description: Service Unavailable
    content:
      "application/problem+json":
        schema:
          $ref: 'https://github.com/sonaemc/api-guidelines/blob/main/models/problem-1.0.1.yaml'
```

`id`\</a\>"\>You may define custom problem types as extensions of the
Problem JSON object if your API needs to return specific, additional,
and more detailed error information.

`id`\</a\>"\>**Note:** Problem `type` and `instance` identifiers in our
APIs are not meant to be resolved.
[RFC 7807](https://tools.ietf.org/html/rfc7807) encourages that problem
types are URI references that point to human-readable documentation,
**but** we deliberately decided against that, as all important parts of
the API must be documented using [OpenAPI](#101) anyway. In addition,
URLs tend to be fragile and not very stable over longer periods because
of organizational and documentation changes and descriptions might
easily get out of sync.

`id`\</a\>"\>In order to stay compatible with
[RFC 7807](https://tools.ietf.org/html/rfc7807) we proposed to use
[relative URI
references](https://tools.ietf.org/html/rfc3986#section-4.1) usually
defined by `absolute-path [ '?' query ] [ '#' fragment ]` as simplified
identifiers in `type` and `instance` fields:

  - `/problems/out-of-stock`

  - `/problems/insufficient-funds`

  - `/problems/user-deactivated`

  - `/problems/connection-error#read-timeout`

`id`\</a\>"\>**Hint:** The use of [absolute
URIs](https://tools.ietf.org/html/rfc3986#section-4.3) is not forbidden
but strongly discouraged. If you use absolute URIs, please reference
[problem-1.0.0.yaml\#/Problem](https://github.com/sonaemc/api-guidelines/blob/main/models/problem-1.0.0.yaml)
instead.

`id`\</a\>"\>Stack traces contain implementation details that are not
part of an API, and on which clients should never rely. Moreover, stack
traces can leak sensitive information that partners and third parties
are not allowed to receive and may disclose insights about
vulnerabilities to attackers.

# Performance

`id`\</a\>"\>APIs should support techniques for reducing bandwidth based
on client needs. This holds for APIs that (might) have high payloads
and/or are used in high-traffic scenarios like the public Internet and
telecommunication networks. Typical examples are APIs used by mobile web
app clients with (often) less bandwidth connectivity.

`id`\</a\>"\>Common techniques include:

  - compression of request and response bodies (see [???](#156))

  - querying field filters to retrieve a subset of resource attributes
    (see [???](#157) below)

  - `ETag` and `If-Match`/`If-None-Match` headers to avoid re-fetching
    of unchanged resources (see [???](#182))

  - `Prefer` header with `return=minimal` or `respond-async` to
    anticipate reduced processing requirements of clients (see
    [???](#181))

  - [Pagination](#pagination) for incremental access of larger
    collections of data items

  - caching of master data items, i.e. resources that change rarely or
    not at all after creation (see [???](#227)).

`id`\</a\>"\>Each of these items is described in greater detail below.

`id`\</a\>"\>Compress the payload of your API’s responses with gzip,
unless there’s a good reason not to — for example, you are serving so
many requests that the time to compress becomes a bottleneck. This helps
to transport data faster over the network (fewer bytes) and makes
frontends respond faster.

`id`\</a\>"\>Though gzip compression might be the default choice for
server payload, the server should also support payload without
compression and its client control via `Accept-Encoding` request
header — see also [RFC 7231 Section
5.3.4](https://tools.ietf.org/html/rfc7231#section-5.3.4). The server
should indicate used gzip compression via the `Content-Encoding` header.

`id`\</a\>"\>Depending on your use case and payload size, you can
significantly reduce network bandwidth need by supporting filtering of
returned entity fields. Here, the client can explicitly determine the
subset of fields he wants to receive via the `fields` query parameter.
(It is analogue to [GraphQL
`fields`](https://graphql.org/learn/queries/#fields) and simple queries,
and also applied, for instance, for [Google Cloud API’s partial
responses](https://cloud.google.com/storage/docs/json_api/v1/how-tos/performance#partial-response).)

## Unfiltered

``` http
GET http://api.example.org/users/123 HTTP/1.1

HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": "cddd5e44-dae0-11e5-8c01-63ed66ab2da5",
  "name": "John Doe",
  "address": "1600 Pennsylvania Avenue Northwest, Washington, DC, United States",
  "birthday": "1984-09-13",
  "friends": [ {
    "id": "1fb43648-dae1-11e5-aa01-1fbc3abb1cd0",
    "name": "Jane Doe",
    "address": "1600 Pennsylvania Avenue Northwest, Washington, DC, United States",
    "birthday": "1988-04-07"
  } ]
}
```

## Filtered

``` http
GET http://api.example.org/users/123?fields=(name,friends(name)) HTTP/1.1

HTTP/1.1 200 OK
Content-Type: application/json

{
  "name": "John Doe",
  "friends": [ {
    "name": "Jane Doe"
  } ]
}
```

`id`\</a\>"\>The `fields` query parameter determines the fields returned
with the response payload object. For instance, `(name)` returns `users`
root object with only the `name` field, and `(name,friends(name))`
returns the `name` and the nested `friends` object with only its `name`
field.

`id`\</a\>"\>Open API doesn’t support you in formally specifying
different return object schemes depending on a parameter. When you
define the field parameter, we recommend to provide the following
description: \`Endpoint supports filtering of return object fields as
described in [???](#157).

`id`\</a\>"\>The syntax of the query `fields` value is defined by the
following [BNF](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form)
grammar.

``` bnf
<fields>            ::= [ <negation> ] <fields_struct>
<fields_struct>     ::= "(" <field_items> ")"
<field_items>       ::= <field> [ "," <field_items> ]
<field>             ::= <field_name> | <fields_substruct>
<fields_substruct>  ::= <field_name> <fields_struct>
<field_name>        ::= <dash_letter_digit> [ <field_name> ]
<dash_letter_digit> ::= <dash> | <letter> | <digit>
<dash>              ::= "-" | "_"
<letter>            ::= "A" | ... | "Z" | "a" | ... | "z"
<digit>             ::= "0" | ... | "9"
<negation>          ::= "!"
```

`id`\</a\>"\>**Note:** Following the [principle of least
astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment),
you should not define the `fields` query parameter using a default
value, as the result is counter-intuitive and very likely not
anticipated by the consumer.

`id`\</a\>"\>Embedding related resources (also know as *Resource
expansion*) is a great way to reduce the number of requests. In cases
where clients know upfront that they need some related resources they
can instruct the server to prefetch that data eagerly. Whether this is
optimized on the server, e.g. a database join, or done in a generic way,
e.g. an HTTP proxy that transparently embeds resources, is up to the
implementation.

`id`\</a\>"\>See [???](#137) for naming, e.g. "embed" for steering of
embedded resource expansion. Please use the
[BNF](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) grammar,
as already defined above for filtering, when it comes to an embedding
query syntax.

`id`\</a\>"\>Embedding a sub-resource can possibly look like this where
an order resource has its order items as sub-resource
(/order/{orderId}/items):

``` http
GET /order/123?embed=(items) HTTP/1.1

{
  "id": "123",
  "_embedded": {
    "items": [
      {
        "position": 1,
        "sku": "1234-ABCD-7890",
        "price": {
          "amount": 71.99,
          "currency": "EUR"
        }
      }
    ]
  }
}
```

`id`\</a\>"\>Caching has to take many aspects into account, e.g. general
[cacheability](#cacheable) of response information, our guideline to
protect endpoints using SSL and [OAuth authorization](#104), resource
update and invalidation rules, existence of multiple consumer instances.
As a consequence, caching is in best case complex, e.g. with respect to
consistency, in worst case inefficient.

`id`\</a\>"\>As a consequence, client side as well as transparent web
caching should be avoided, unless the service supports and requires it
to protect itself, e.g. in case of a heavily used and therefore rate
limited master data service, i.e. data items that rarely or not at all
change after creation.

`id`\</a\>"\>As default, API providers and consumers should always set
the `Cache-Control` header set to `Cache-Control: no-store` and assume
the same setting, if no `Cache-Control` header is provided.

`id`\</a\>"\>**Note:** There is no need to document this default
setting. However, please make sure that your framework is attaching this
header value by default, or ensure this manually, e.g. using the best
practice of Spring Security as shown below. Any setup deviating from
this default must be sufficiently documented.

``` http
Cache-Control: no-cache, no-store, must-revalidate, max-age=0
```

`id`\</a\>"\>If your service really requires to support caching, please
observe the following rules:

  - Document all [cacheable](#cacheable) `GET`, `HEAD`, and `POST`
    endpoints by declaring the support of `Cache-Control`, `Vary`, and
    `ETag` headers in response. **Note:** you must not define the
    `Expires` header to prevent redundant and ambiguous definition of
    cache lifetime. A sensible default documentation of these headers is
    given below.

  - Take care to specify the ability to support caching by defining the
    right caching boundaries, i.e. time-to-live and cache constraints,
    by providing sensible values for `Cache-Control` and `Vary` in your
    service. We will explain best practices below.

  - Provide efficient methods to warm up and update caches, e.g. as
    follows:
    
      - In general, you should support [`ETag` Together With `If-Match`/
        `If-None-Match` Header](#182) on all [cacheable](#cacheable)
        endpoints.
    
      - For larger data items support `HEAD` requests or more efficient
        `GET` requests with `If-None-Match` header to check for updates.
    
      - For small data sets provide full collection `GET` requests
        supporting `ETag`, as well as `HEAD` requests or `GET` requests
        with `If-None-Match` to check for updates.
    
      - For medium sized data sets provide full collection `GET`
        requests supporting `ETag` together with
        [Pagination](#pagination) and `<entity-tag>` filtering `GET`
        requests for limiting the response to changes since the provided
        `<entity-tag>`. **Note:** this is not supported by generic
        client and proxy caches on HTTP layer.

`id`\</a\>"\>**Hint:** For proper cache support, you must return 304
without content on a failed `HEAD` or `GET` request with
[`If-None-Match: <entity-tag>`](#182) instead of 412.

``` yaml
components:
  headers:
  - Cache-Control:
      description: |
        The RFC 7234 Cache-Control header field is providing directives to
        control how proxies and clients are allowed to cache responses results
        for performance. Clients and proxies are free to not support caching of
        results, however if they do, they must obey all directives mentioned in
        [RFC-7234 Section 5.2.2](https://tools.ietf.org/html/rfc7234) to the
        word.

        In case of caching, the directive provides the scope of the cache
        entry, i.e. only for the original user (private) or shared between all
        users (public), the lifetime of the cache entry in seconds (max-age),
        and the strategy how to handle a stale cache entry (must-revalidate).
        Please note, that the lifetime and validation directives for shared
        caches are different (s-maxage, proxy-revalidate).

      type: string
      required: false
      example: "private, must-revalidate, max-age=300"

  - Vary:
      description: |
        The RFC 7231 Vary header field in a response defines which parts of
        a request message, aside the target URL and HTTP method, might have
        influenced the response. A client or proxy cache must respect this
        information, to ensure that it delivers the correct cache entry (see
        [RFC-7231 Section
        7.1.4](https://tools.ietf.org/html/rfc7231#section-7.1.4)).

      type: string
      required: false
      example: "accept-encoding, accept-language"
```

`id`\</a\>"\>**Hint:** For `ETag` source see [???](#182).

`id`\</a\>"\>The default setting for `Cache-Control` should contain the
`private` directive for endpoints with standard [OAuth
authorization](#104), as well as the `must-revalidate` directive to
ensure, that the client does not use stale cache entries. Last, the
`max-age` directive should be set to a value between a few seconds
(`max-age=60`) and a few hours (`max-age=86400`) depending on the change
rate of your master data and your requirements to keep clients
consistent.

``` http
Cache-Control: private, must-revalidate, max-age=300
```

`id`\</a\>"\>The default setting for `Vary` is harder to determine
correctly. It highly depends on the API endpoint, e.g. whether it
supports compression, accepts different media types, or requires other
request specific headers. To support correct caching you have to
carefully choose the value. However, a good first default may be:

``` http
Vary: accept, accept-encoding
```

`id`\</a\>"\>Anyhow, this is only relevant, if you encourage clients to
install generic HTTP layer client and proxy caches.

`id`\</a\>"\>**Note:** generic client and proxy caching on HTTP level is
hard to configure. Therefore, we strongly recommend to attach the
(possibly distributed) cache directly to the service (or gateway) layer
of your application. This relieves from interpreting the `Vary` header
and greatly simplifies interpreting the `Cache-Control` and `ETag`
headers. Moreover, is highly efficient with respect to caching
performance and overhead, and allows to support more [advanced cache
update and warm up patterns](#cache-support-patterns).

`id`\</a\>"\>Anyhow, please carefully read
[RFC 7234](https://tools.ietf.org/html/rfc7234) before adding any client
or proxy cache.

# Pagination

`id`\</a\>"\>Access to lists of data items must support pagination to
protect the service against overload as well as for best client side
iteration and batch processing experience. This holds true for all lists
that are (potentially) larger than just a few hundred entries.

`id`\</a\>"\>There are two well known page iteration techniques:

  - [Offset/Limit-based
    pagination](https://developer.infoconnect.com/paging-results):
    numeric offset identifies the first page entry

  - [Cursor/Limit-based](https://dev.twitter.com/overview/api/cursoring)
    — aka key-based — pagination: a unique key element identifies the
    first page entry (see also [Facebook’s
    guide](https://developers.facebook.com/docs/graph-api/using-graph-api/v2.4#paging))

`id`\</a\>"\>The technical conception of pagination should also consider
user experience related issues. As mentioned in this
[article](https://www.smashingmagazine.com/2016/03/pagination-infinite-scrolling-load-more-buttons/),
jumping to a specific page is far less used than navigation via
`next`/`prev` page links (See [???](#161)). This favours cursor-based
over offset-based pagination.

`id`\</a\>"\>**Note:** To provide a consistent look and feel of
pagination patterns, you must stick to the common query parameter names
defined in [???](#137).

`id`\</a\>"\>Cursor-based pagination is usually better and more
efficient when compared to offset-based pagination. Especially when it
comes to high-data volumes and/or storage in NoSQL databases.

`id`\</a\>"\>Before choosing cursor-based pagination, consider the
following trade-offs:

  - Usability/framework support:
    
      - Offset-based pagination is more widely known than cursor-based
        pagination, so it has more framework support and is easier to
        use for API clients

  - Use case - jump to a certain page:
    
      - If jumping to a particular page in a range (e.g., 51 of 100) is
        really a required use case, cursor-based navigation is not
        feasible.

  - Data changes may lead to anomalies in result pages:
    
      - Offset-based pagination may create duplicates or lead to missing
        entries if rows are inserted or deleted between two subsequent
        paging requests.
    
      - If implemented incorrectly, cursor-based pagination may fail
        when the cursor entry has been deleted before fetching the
        pages.

  - Performance considerations - efficient server-side processing using
    offset-based pagination is hardly feasible for:
    
      - Very big data sets, especially if they cannot reside in the main
        memory of the database.
    
      - Sharded or NoSQL databases.

  - Cursor-based navigation may not work if you need the total count of
    results.

`id`\</a\>"\>The `cursor` used for pagination is an opaque pointer to a
page, that must never be **inspected** or **constructed** by clients. It
usually encodes (encrypts) the page position, i.e. the identifier of the
first or last page element, the pagination direction, and the applied
query filters - or a hash over these - to safely recreate the collection
(see also [Cursor-based pagination in RESTful
APIs](#cursor-based-pagination)).

`id`\</a\>"\>To simplify client design, APIs should support [simplified
hypertext controls](#165) for paginating over collections whenever
applicable as follows (see also [Pagination fields](#pagination-fields)
for details):

``` json
{
  "self": "http://my-service.sonaemc-apis.com/v1/resources?cursor=<self-position>",
  "first": "http://my-service.sonaemc-apis.com/v1/resources?cursor=<first-position>",
  "prev": "http://my-service.sonaemc-apis.com/v1/resources?cursor=<previous-position>",
  "next": "http://my-service.sonaemc-apis.com/v1/resources?cursor=<next-position>",
  "last": "http://my-service.sonaemc-apis.com/v1/resources?cursor=<last-position>",
  "query": {
    "query-param-": ...,
    "query-param-<n>": ...
  },
  "items": [...]
}
```

`id`\</a\>"\>**Remark:** You should avoid providing a total count unless
there is a clear need to do so. Very often, there are significant system
and performance implications when supporting full counts. Especially, if
the data set grows and requests become complex queries and filters drive
full scans. While this is an implementation detail relative to the API,
it is important to consider the ability to support serving counts over
the life of a service.

# Hypermedia

`id`\</a\>"\>We strive for a good implementation of [REST Maturity Level
2](http://martinfowler.com/articles/richardsonMaturityModel.html#level2)
as it enables us to build resource-oriented APIs that make full use of
HTTP verbs and status codes. You can see this expressed by many rules
throughout these guidelines, e.g.:

  - [???](#138)

  - [???](#141)

  - [???](#148)

  - [???](#150)

`id`\</a\>"\>Although this is not HATEOAS, it should not prevent you
from designing proper link relationships in your APIs as stated in rules
below.

`id`\</a\>"\>We do not generally recommend to implement [REST Maturity
Level
3](http://martinfowler.com/articles/richardsonMaturityModel.html#level3).
HATEOAS comes with additional API complexity without real value in our
context.

`id`\</a\>"\>Our major concerns regarding the promised advantages of
HATEOAS (see also [RESTistential Crisis over Hypermedia
APIs](https://www.infoq.com/news/2014/03/rest-at-odds-with-web-apis),
[Why I Hate
HATEOAS](https://jeffknupp.com/blog/2014/06/03/why-i-hate-hateoas/) and
others for a detailed discussion):

  - We follow the [API First principle](#100) with APIs explicitly
    defined outside the code with standard specification language.
    HATEOAS does not really add value for SOA client engineers in terms
    of API self-descriptiveness: a client engineer finds necessary links
    and usage description (depending on resource state) in the API
    reference definition anyway.

  - Generic HATEOAS clients which need no prior knowledge about APIs and
    explore API capabilities based on hypermedia information provided,
    is a theoretical concept that we haven’t seen working in practice
    and does not fit to our SOA set-up. The Open API description format
    (and tooling based on Open API) doesn’t provide sufficient support
    for HATEOAS either.

  - In practice relevant HATEOAS approximations (e.g. following
    specifications like HAL or JSON API) support API navigation by
    abstracting from URL endpoint and HTTP method aspects via link
    types. So, Hypermedia does not prevent clients from required manual
    changes when domain model changes over time.

  - Hypermedia make sense for humans, less for SOA machine clients. We
    would expect use cases where it may provide value more likely in the
    frontend and human facing service domain.

  - Hypermedia does not prevent API clients to implement shortcuts and
    directly target resources without *discovering* them.

`id`\</a\>"\>However, we do not forbid HATEOAS; you could use it, if you
checked its limitations and still see clear value for your usage
scenario that justifies its additional complexity. If you use HATEOAS
please share experience and present your findings in the [API Guild
\[internal link](https://…/display/GUL/API+Guild)\].

`id`\</a\>"\>Links to other resource must always use full, absolute URI.

`id`\</a\>"\>**Motivation**: Exposing any form of relative URI (no
matter if the relative URI uses an absolute or relative path) introduces
avoidable client side complexity. It also requires clarity on the base
URI, which might not be given when using features like embedding
subresources. The primary advantage of non-absolute URI is reduction of
the payload size, which is better achievable by following the
recommendation to use [gzip compression](#156)

`id`\</a\>"\>When embedding links to other resources into
representations you must use the common hypertext control object. It
contains at least one attribute:

  - `href`: The URI of the resource the hypertext control is linking to.
    All our API are using HTTP(s) as URI scheme.

`id`\</a\>"\>In API that contain any hypertext controls, the attribute
name `href` is reserved for usage within hypertext controls.

`id`\</a\>"\>The schema for hypertext controls can be derived from this
model:

``` yaml
HttpLink:
  description: A base type of objects representing links to resources.
  type: object
  properties:
    href:
      description: Any URI that is using http or https protocol
      type: string
      format: uri
  required:
    - href
```

`id`\</a\>"\>The name of an attribute holding such a `HttpLink` object
specifies the relation between the object that contains the link and the
linked resource. Implementations should use names from the [IANA Link
Relation Registry](http://www.iana.org/assignments/link-relations)
whenever appropriate. As IANA link relation names use hyphen-case
notation, while this guide enforces snake\_case notation for attribute
names, hyphens in IANA names have to be replaced with underscores (e.g.
the IANA link relation type `version-history` would become the attribute
`version_history`)

`id`\</a\>"\>Specific link objects may extend the basic link type with
additional attributes, to give additional information related to the
linked resource or the relationship between the source resource and the
linked one.

`id`\</a\>"\>E.g. a service providing "Person" resources could model a
person who is married with some other person with a hypertext control
that contains attributes which describe the other person (`id`, `name`)
but also the relationship "spouse" between the two persons (`since`):

``` json
{
  "id": "446f9876-e89b-12d3-a456-426655440000",
  "name": "Peter Mustermann",
  "spouse": {
    "href": "https://...",
    "since": "1996-12-19",
    "id": "123e4567-e89b-12d3-a456-426655440000",
    "name": "Linda Mustermann"
  }
}
```

`id`\</a\>"\>Hypertext controls are allowed anywhere within a JSON
model. While this specification would allow
[HAL](http://stateless.co/hal_specification.html), we actually don’t
recommend/enforce the usage of HAL anymore as the structural separation
of meta-data and data creates more harm than value to the
understandability and usability of an API.

`id`\</a\>"\>For pagination and self-references a simplified form of the
[extensible common hypertext controls](#164) should be used to reduce
the specification and cognitive overhead. It consists of a simple URI
value in combination with the corresponding [link
relations](http://www.iana.org/assignments/link-relations), e.g. `next`,
`prev`, `first`, `last`, or `self`.

`id`\</a\>"\>See [???](#164) and [???](#161) for more information and
examples.

`id`\</a\>"\>For flexibility and precision, we prefer links to be
directly embedded in the JSON payload instead of being attached using
the uncommon link header syntax. As a result, the use of the [`Link`
Header defined by RFC
8288](https://tools.ietf.org/html/rfc8288#section-3) in conjunction with
JSON media types is forbidden.

# Standard headers

`id`\</a\>"\>This section describes a handful of standard headers, which
we found raising the most questions in our daily usage, or which are
useful in particular circumstances but not widely known.

`id`\</a\>"\>Use [this
list](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields) and
explicitly mention its support in your Open API definition.

`id`\</a\>"\>This convention is followed by most standard headers e.g.
as defined in [RFC 2616](https://tools.ietf.org/html/rfc2616) and
[RFC 4229](https://tools.ietf.org/html/rfc4229). Examples:

``` http
If-Modified-Since
Accept-Encoding
Content-ID
Language
```

`id`\</a\>"\>Note, HTTP standard defines headers as case-insensitive
([RFC 7230, p.22](https://tools.ietf.org/html/rfc7230#page-22)).
However, for sake of readability and consistency you should follow the
convention when using standard or proprietary headers. Exceptions are
common abbreviations like `ID`.

`id`\</a\>"\>Content or entity headers are headers with a `Content-`
prefix. They describe the content of the body of the message and they
can be used in both, HTTP requests and responses. Commonly used content
headers include but are not limited to:

  - `Content-Disposition` can indicate that the representation is
    supposed to be saved as a file, and the proposed file name.

  - `Content-Encoding` indicates compression or encryption algorithms
    applied to the content.

  - `Content-Length` indicates the length of the content (in bytes).

  - `Content-Language` indicates that the body is meant for people
    literate in some human language(s).

  - `Content-Location` indicates where the body can be found otherwise
    ([???](#179) for more details\]).

  - `Content-Range` is used in responses to range requests to indicate
    which part of the requested resource representation is delivered
    with the body.

  - `Content-Type` indicates the media type of the body content.

`id`\</a\>"\>As the correct usage of `Content-Location` response header
(see below) with respect to caching and its method specific semantics is
difficult, we *discourage* the use of `Content-Location`. In most cases
it is sufficient to inform clients about the resource location in create
or re-direct responses by using the `Location` header while avoiding the
`Content-Location` specific ambiguities and complexities.

`id`\</a\>"\>More details in RFC 7231 [7.1.2
Location](https://tools.ietf.org/html/rfc7231#section-7.1.2), [3.1.4.2
Content-Location](https://tools.ietf.org/html/rfc7231#section-3.1.4.2)

`id`\</a\>"\>The `Content-Location` header is *optional* and can be used
in successful write operations (`PUT`, `POST`, or `PATCH`) or read
operations (`GET`, `HEAD`) to guide caching and signal a receiver the
actual location of the resource transmitted in the response body. This
allows clients to identify the resource and to update their local copy
when receiving a response with this header.

`id`\</a\>"\>The Content-Location header can be used to support the
following use cases:

  - For reading operations `GET` and `HEAD`, a different location than
    the requested URI can be used to indicate that the returned resource
    is subject to content negotiations, and that the value provides a
    more specific identifier of the resource.

  - For writing operations `PUT` and `PATCH`, an identical location to
    the requested URI can be used to explicitly indicate that the
    returned resource is the current representation of the newly created
    or updated resource.

  - For writing operations `POST` and `DELETE`, a content location can
    be used to indicate that the body contains a status report resource
    in response to the requested action, which is available at provided
    location.

`id`\</a\>"\>**Note**: When using the `Content-Location` header, the
`Content-Type` header has to be set as well. For example:

``` http
GET /products/123/images HTTP/1.1

HTTP/1.1 200 OK
Content-Type: image/png
Content-Location: /products/123/images?format=raw
```

`id`\</a\>"\>The `Prefer` header defined in
[RFC 7240](https://tools.ietf.org/html/rfc7240) allows clients to
request processing behaviors from servers. It pre-defines a number of
preferences and is extensible, to allow others to be defined. Support
for the `Prefer` header is entirely optional and at the discretion of
API designers, but as an existing Internet Standard, is recommended over
defining proprietary "X-" headers for processing directives.

`id`\</a\>"\>The `Prefer` header can defined like this in an API
definition:

``` yaml
components:
  headers:
  - Prefer:
      description: >
        The RFC7240 Prefer header indicates that a particular server behavior
        is preferred by the client but is not required for successful completion
        of the request (see [RFC 7240](https://tools.ietf.org/html/rfc7240).
        The following behaviors are supported by this API:

        # (indicate the preferences supported by the API or API endpoint)
        * **respond-async** is used to suggest the server to respond as fast as
          possible asynchronously using 202 - accepted - instead of waiting for
          the result.
        * **return=<minimal|representation>** is used to suggest the server to
          return using 204 without resource (minimal) or using 200 or 201 with
          resource (representation) in the response body on success.
        * **wait=<delta-seconds>** is used to suggest a maximum time the server
          has time to process the request synchronously.
        * **handling=<strict|lenient>** is used to suggest the server to be
          strict and report error conditions or lenient, i.e. robust and try to
          continue, if possible.

      type: array
      items:
        type: string
      required: false
```

`id`\</a\>"\>**Note:** Please copy only the behaviors into your `Prefer`
header specification that are supported by your API endpoint. If
necessary, specify different `Prefer` headers for each supported use
case.

`id`\</a\>"\>Supporting APIs may return the `Preference-Applied` header
also defined in [RFC 7240](https://tools.ietf.org/html/rfc7240) to
indicate whether a preference has been applied.

`id`\</a\>"\>When creating or updating resources it may be necessary to
expose conflicts and to prevent the *lost update* or *initially created*
problem. Following [RFC 7232 "HTTP: Conditional
Requests"](https://tools.ietf.org/html/rfc7232) this can be best
accomplished by supporting the `ETag` header together with the
`If-Match` or `If-None-Match` conditional header. The contents of an
`ETag: <entity-tag>` header is either (a) a hash of the response body,
(b) a hash of the last modified field of the entity, or (c) a version
number or identifier of the entity version.

`id`\</a\>"\>To expose conflicts between concurrent update operations
via `PUT`, `POST`, or `PATCH`, the `If-Match: <entity-tag>` header can
be used to force the server to check whether the version of the updated
entity is conforming to the requested `<entity-tag>`. If no matching
entity is found, the operation is supposed a to respond with status code
412 - precondition failed.

`id`\</a\>"\>Beside other use cases, `If-None-Match: *` can be used in a
similar way to expose conflicts in resource creation. If any matching
entity is found, the operation is supposed a to respond with status code
412 - precondition failed.

`id`\</a\>"\>The `ETag`, `If-Match`, and `If-None-Match` headers can be
defined as follows in the API definition:

``` yaml
components:
  headers:
  - ETag:
      description: |
        The RFC 7232 ETag header field in a response provides the entity-tag of
        a selected resource. The entity-tag is an opaque identifier for versions
        and representations of the same resource over time, regardless whether
        multiple versions are valid at the same time. An entity-tag consists of
        an opaque quoted string, possibly prefixed by a weakness indicator (see
        [RFC 7232 Section 2.3](https://tools.ietf.org/html/rfc7232#section-2.3).

      type: string
      required: false
      example: W/"xy", "5", "5db68c06-1a68-11e9-8341-68f728c1ba70"

  - If-Match:
      description: |
        The RFC7232 If-Match header field in a request requires the server to
        only operate on the resource that matches at least one of the provided
        entity-tags. This allows clients express a precondition that prevent
        the method from being applied if there have been any changes to the
        resource (see [RFC 7232 Section
        3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

      type: string
      required: false
      example: "5", "7da7a728-f910-11e6-942a-68f728c1ba70"

  - If-None-Match:
      description: |
        The RFC7232 If-None-Match header field in a request requires the server
        to only operate on the resource if it does not match any of the provided
        entity-tags. If the provided entity-tag is `*`, it is required that the
        resource does not exist at all (see [RFC 7232 Section
        3.2](https://tools.ietf.org/html/rfc7232#section-3.2).

      type: string
      required: false
      example: "7da7a728-f910-11e6-942a-68f728c1ba70", *
```

`id`\</a\>"\>Please see [Optimistic locking in RESTful
APIs](#optimistic-locking) for a detailed discussion and options.

`id`\</a\>"\>When creating or updating resources it can be helpful or
necessary to ensure a strong [idempotent](#idempotent) behavior
comprising same responses, to prevent duplicate execution in case of
retries after timeout and network outages. Generally, this can be
achieved by sending a client specific *unique request key* – that is not
part of the resource – via `Idempotency-Key` header.

`id`\</a\>"\>The *unique request key* is stored temporarily, e.g. for 24
hours, together with the response and the request hash (optionally) of
the first request in a key cache, regardless of whether it succeeded or
failed. The service can now look up the *unique request key* in the key
cache and serve the response from the key cache, instead of re-executing
the request, to ensure [idempotent](#idempotent) behavior. Optionally,
it can check the request hash for consistency before serving the
response. If the key is not in the key store, the request is executed as
usual and the response is stored in the key cache.

`id`\</a\>"\>This allows clients to safely retry requests after
timeouts, network outages, etc. while receive the same response multiple
times. **Note:** The request retry in this context requires to send the
exact same request, i.e. updates of the request that would change the
result are off-limits. The request hash in the key cache can protection
against this misbehavior. The service is recommended to reject such a
request using status code 400.

`id`\</a\>"\>**Important:** To grant a reliable
[idempotent](#idempotent) execution semantic, the resource and the key
cache have to be updated with hard transaction semantics – considering
all potential pitfalls of failures, timeouts, and concurrent requests in
a distributed systems. This makes a correct implementation exceeding the
local context very hard.

`id`\</a\>"\>The `Idempotency-Key` header must be defined as follows,
but you are free to choose your expiration time:

``` yaml
components:
  headers:
  - Idempotency-Key:
      description: |
        The idempotency key is a free identifier created by the client to
        identify a request. It is used by the service to identify subsequent
        retries of the same request and ensure idempotent behavior by sending
        the same response without executing the request a second time.

        Clients should be careful as any subsequent requests with the same key
        may return the same response without further check. Therefore, it is
        recommended to use an UUID version 4 (random) or any other random
        string with enough entropy to avoid collisions.

        Idempotency keys expire after 24 hours. Clients are responsible to stay
        within this limits, if they require idempotent behavior.

      type: string
      format: uuid
      required: false
      example: "7da7a728-f910-11e6-942a-68f728c1ba70"
```

`id`\</a\>"\>**Hint:** The key cache is not intended as request log, and
therefore should have a limited lifetime, else it could easily exceed
the data resource in size.

`id`\</a\>"\>**Note:** The `Idempotency-Key` header unlike other headers
in this section is not standardized in an RFC. Our only reference are
the usage in the [Stripe
API](https://stripe.com/docs/api/idempotent_requests). However, as it
fit not into our section about [Proprietary
headers](#proprietary-headers), and we did not want to change the header
name and semantic, we decided to treat it as any other common header.

# Proprietary headers

`id`\</a\>"\>This section shares definitions of proprietary headers that
should be named consistently because they address overarching
service-related concerns. Whether services support these concerns or not
is optional; therefore, the Open API API specification is the right
place to make this explicitly visible. Use the parameter definitions of
the resource HTTP methods.

`id`\</a\>"\>As a general rule, proprietary HTTP headers should be
avoided. From a conceptual point of view, the business semantics and
intent of an operation should always be expressed via the URLs path and
query parameters, the method, and the content, but not via proprietary
headers. Headers are typically used to implement protocol processing
aspects, such as flow control, content negotiation, and authentication,
and represent business agnostic request modifiers that provide generic
context information
([RFC 7231](https://tools.ietf.org/html/rfc7231#section-5)).

`id`\</a\>"\>However, the exceptional usage of proprietary headers is
still helpful when domain-specific generic context information…

1.  needs to be passed end to end along the service call chain (even if
    not all called services use it as input for steering service
    behavior e.g. `x-sales-channel` header) and/or…

2.  is provided by specific gateway components

`id`\</a\>"\>Below, we explicitly define the list of proprietary header
exceptions usable for all services for passing through generic context
information of our fashion domain (use case a).

`id`\</a\>"\>Per convention, non standardized, proprietary header names
are prefixed with `X-`. (We do not follow the Internet Engineering Task
Force’s recommendation in
[RFC 6648](https://tools.ietf.org/html/rfc6648) to deprecate usage of
`X-` headers.) Remember that HTTP header field names are not
case-sensitive:

| Header field name | Type   | Description                                                                                                                                                                                                                                                                                                                                                                           | Header field value example           |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| `X-Flow-ID`       | String | For more information see [???](#233).                                                                                                                                                                                                                                                                                                                                                 | GKY7oDhpSiKY\_gAAAABZ\_A             |
| `X-Tenant-ID`     | String | Identifies the tenant that initiated the request to the multi tenant Sonae MC Platform.                                                                                                                                                                                                                                                                                               | 9f8b3ca3-4be5-436c-a847-9cd55460c495 |
| `X-Sales-Channel` | String | Sales channels are owned by retailers and represent a specific consumer segment being addressed with a specific product assortment that is offered via CFA retailer catalogs to consumers (see [platform glossary (internal link)](https://…/glossary/glossary.html)).                                                                                                                | 52b96501-0f8d-43e7-82aa-8a96fab134d7 |
| `X-Frontend-Type` | String | Consumer facing applications (CFAs) provide business experience to their customers via different frontend application types, for instance, mobile app or browser. Info should be passed-through as generic aspect — there are diverse concerns, e.g. pushing mobiles with specific coupons, that make use of it. Current range is mobile-app, browser, facebook-app, chat-app, email. | mobile-app                           |
| `X-device-Type`   | String | There are also use cases for steering customer experience (incl. features and content) depending on device type. Via this header info should be passed-through as generic aspect. Current range is smartphone, tablet, desktop, other.                                                                                                                                                | tablet                               |
| `X-device-OS`     | String | On top of device type above, we even want to differ between device platform, e.g. smartphone Android vs. iOS. Via this header info should be passed-through as generic aspect. Current range is iOS, Android, Windows, Linux, MacOS.                                                                                                                                                  | Android                              |

`id`\</a\>"\>**Exception:** The only exception to this guideline are the
conventional hop-by-hop `X-RateLimit-` headers which can be used as
defined in [???](#153).

`id`\</a\>"\>As part of the guidelines we sourced the OpenAPI definition
of all proprietary headers; you can simply reference it when defining
the API endpoint requests e.g.

``` yaml
parameters:
- $ref: "https://github.com/sonaemc/api-guidelines/blob/main/models/request-headers-1.0.0.yaml#/X-Flow-ID"
- $ref: "https://github.com/sonaemc/api-guidelines/blob/main/models/request-headers-1.0.0.yaml#/X-Tenant-ID"
```

`id`\</a\>"\>Response headers can be referenced in the API endpoint e.g.

``` yaml
parameters:
- $ref: "https://github.com/sonaemc/api-guidelines/blob/main/models/response-headers-1.0.0.yaml#/ETag"
- $ref: "https://github.com/sonaemc/api-guidelines/blob/main/models/response-headers-1.0.0.yaml#/Cache-Control"
```

`id`\</a\>"\>All Sonae MC’s proprietary headers listed above are
end-to-end headers \[2\] and must be propagated to the services down the
call chain. The header names and values must remain unchanged.

`id`\</a\>"\>For example, the values of the custom headers like
`X-Device-Type` can affect the results of queries by using device type
information to influence recommendation results. Besides, the values of
the custom headers can influence the results of the queries (e.g. the
device type information influences the recommendation results).

`id`\</a\>"\>Sometimes the value of a proprietary header will be used as
part of the entity in a subsequent request. In such cases, the
proprietary headers must still be propagated as headers with the
subsequent request, despite the duplication of information.

`id`\</a\>"\>The *Flow-ID* is a generic parameter to be passed through
service APIs and written into log files and traces. A consequent usage
of the *Flow-ID* facilitates the tracking of call flows through our
system and allows the correlation of service activities initiated by a
specific call. This is extremely helpful for operational troubleshooting
and log analysis. Main use case of *Flow-ID* is to track service calls
of our SaaS fashion commerce platform and initiated internal processing
flows (executed synchronously via APIs).

## Data Definition

`id`\</a\>"\>The *Flow-ID* must be passed through:

  - RESTful API requests via `X-Flow-ID` proprietary header (see
    [???](#184))

`id`\</a\>"\>The following formats are allowed:

  - `UUID` ([RFC-4122](https://tools.ietf.org/html/rfc4122))

  - `base64` ([RFC-4648](https://tools.ietf.org/html/rfc4648))

  - `base64url` ([RFC-4648
    Section 5](https://tools.ietf.org/html/rfc4648#section-5))

  - Random unique string restricted to the character set
    `[a-zA-Z0-9/+_-=]` maximal of 128 characters.

`id`\</a\>"\>**Note:** If a legacy subsystem can only process *Flow-IDs*
with a specific format or length, it must define this restrictions in
its API specification, and be generous and remove invalid characters or
cut the length to the supported limit.

## Service Guidance

  - Services **must** support *Flow-ID* as generic input, i.e.
    
      - RESTful API endpoints **must** support `X-Flow-ID` header in
        requests
    
    `id`\</a\>"\>**Note:** API-Clients **must** provide *Flow-ID* when
    calling a service If no *Flow-ID* is provided in a request, the
    service must create a new *Flow-ID*.

  - Services **must** propagate *Flow-ID*, i.e. use *Flow-ID* received
    with API-Calls as…
    
      - input for all API called
    
      - data field written for logging and tracing

# API Operation

`id`\</a\>"\>All service applications must publish Open API
specifications of their **Domain** or **Experience** APIs. While this is
optional for **system** APIs, i.e. APIs marked with the
**component-internal**, we still recommend to do so to profit from the
API management infrastructure.

`id`\</a\>"\>An API is published by branching Sonae MC api-specs github
repository, crafting the API and Pull Request the changes to the develop
branch. The repository must only contain **self-contained JSON files**
that each describe one API Resource.

`id`\</a\>"\>Background: In our dynamic and complex service
infrastructure, it is important to provide API client developers a
central place with online access to the API specifications of all
running applications. As a part of the infrastructure, the API
publishing process is used to detect API specifications. The findings
are published in the API Portal - the universal hub for all Sonae MC
APIs.

`id`\</a\>"\>**Note:** To publish an API, it is still necessary to
deploy the artifact successful, as we focus the discovery experience on
APIs supported by running services.

`id`\</a\>"\>Owners of APIs used in production should monitor API
service to get information about its using clients. This information,
for instance, is useful to identify potential review partner for API
changes.

`id`\</a\>"\>Hint: A preferred way of client detection implementation is
by logging of the client-id retrieved from the OAuth token.

# References

`id`\</a\>"\>This section collects links to documents to which we refer,
and base our guidelines on.

# Open API specification

  - **[Open API
    specification](https://github.com/OAI/OpenAPI-Specification/)**

  - **[Open API specification mind
    map](https://openapi-map.apihandyman.io/)**

# Publications, specifications and standards

  - **[RFC 3339](https://tools.ietf.org/html/rfc3339):** Date and Time
    on the Internet: Timestamps

  - **[RFC 4122](https://tools.ietf.org/html/rfc4122):** A Universally
    Unique IDentifier (UUID) URN Namespace

  - **[RFC 4627](https://tools.ietf.org/html/rfc4627):** The
    application/json Media Type for JavaScript Object Notation (JSON)

  - **[RFC 8288](https://tools.ietf.org/html/rfc8288):** Web Linking

  - **[RFC 6585](https://tools.ietf.org/html/rfc6585):** Additional HTTP
    Status Codes

  - **[RFC 6902](https://tools.ietf.org/html/rfc6902):** JavaScript
    Object Notation (JSON) Patch

  - **[RFC 7159](https://tools.ietf.org/html/rfc7159):** The JavaScript
    Object Notation (JSON) Data Interchange Format

  - **[RFC 7230](https://tools.ietf.org/html/rfc7230):** Hypertext
    Transfer Protocol (HTTP/1.1): Message Syntax and Routing

  - **[RFC 7231](https://tools.ietf.org/html/rfc7231):** Hypertext
    Transfer Protocol (HTTP/1.1): Semantics and Content

  - **[RFC 7232](https://tools.ietf.org/html/rfc7232):** Hypertext
    Transfer Protocol (HTTP/1.1): Conditional Requests

  - **[RFC 7233](https://tools.ietf.org/html/rfc7233):** Hypertext
    Transfer Protocol (HTTP/1.1): Range Requests

  - **[RFC 7234](https://tools.ietf.org/html/rfc7234):** Hypertext
    Transfer Protocol (HTTP/1.1): Caching

  - **[RFC 7240](https://tools.ietf.org/html/rfc7240):** Prefer Header
    for HTTP

  - **[RFC 7396](https://tools.ietf.org/html/rfc7396):** JSON Merge
    Patch

  - **[RFC 7807](https://tools.ietf.org/html/rfc7807):** Problem Details
    for HTTP APIs

  - **[RFC 4648](https://tools.ietf.org/html/rfc4648):** The Base16,
    Base32, and Base64 Data Encodings

  - **[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601):** Date and
    time format

  - **[ISO 3166-1
    alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2):** Two
    letter country codes

  - **[ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes):**
    Two letter language codes

  - **[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217):** Currency
    codes

  - **[BCP 47](https://tools.ietf.org/html/bcp47):** Tags for
    Identifying Languages

# Dissertations

  - **[Roy Thomas Fielding - Architectural Styles and the Design of
    Network-Based Software
    Architectures](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm):**
    This is the text which defines what REST is.

# Books

  - **[REST in Practice: Hypermedia and Systems
    Architecture](http://www.amazon.de/REST-Practice-Hypermedia-Systems-Architecture/dp/0596805829)**

  - **[Build APIs You Won’t
    Hate](https://leanpub.com/build-apis-you-wont-hate)**

  - **[InfoQ eBook - Web APIs: From Start to
    Finish](http://www.infoq.com/minibooks/emag-web-api)**

# Blogs

  - **[Lessons-learned blog: Thoughts on RESTful API
    Design](http://restful-api-design.readthedocs.org/en/latest/)**

# Best practices

`id`\</a\>"\>The best practices presented in this section are not part
of the actual guidelines, but should provide guidance for common
challenges we face when implementing RESTful APIs.

# Cursor-based pagination in RESTful APIs

`id`\</a\>"\>Cursor-based pagination is a very powerful and valuable
technique, that allows to efficiently provide a stable view on changing
data. This is obtained by using an anchor element that allows to
retrieve all page elements directly via an ordering combined-index,
usually based on `created_at` or `modified_at`. Simple said, the cursor
is the information set needed to reconstruct the database query to
retrieves the minimal page information from the data storage.

`id`\</a\>"\>The `cursor` itself is an opaque string, transmitted forth
and back between service and clients, that must never be **inspected**
or **constructed** by clients. Therefore, it is good practice to encode
(encrypt) its content in a non-human-readable form.

`id`\</a\>"\>The `cursor` content usually consists of a pointer to the
anchor element defining the page position in the collection, a flag
whether the element is included or excluded into/from the page, the
retrieval direction, and a hash over the applied query filters (or the
query filter itself) to safely re-create the collection. It is important
to note, that a `cursor` should be always defined in relation to the
current page to anticipate all occurring changes when progressing.

`id`\</a\>"\>The `cursor` is usually defined as an encoding of the
following information:

``` yaml
Cursor:
  descriptions: >
    Cursor structure that contains all necessary information to efficiently
    retrieve a page from the data store.
  type: object
  properties:
    position:
      description: >
        Object containing the keys pointing to the anchor element that is
        defining the collection resource page. Normally the position is given
        by the first or the last page element. The position object contains all
        values required to access the element efficiently via the ordered,
        combined index, e.g `modified_at`, `id`.
      type: object
      properties: ...

    element:
      description: >
        Flag whether the anchor element, which is pointed to by the `position`,
        should be *included* or *excluded* from the result set. Normally, only
        the current page includes the pointed to element, while all others are
        exclude it.
      type: string
      enum: [ INCLUDED, EXCLUDED ]

    direction:
      description: >
        Flag for the retrieval direction that is defining which elements to
        choose from the collection resource starting from the anchor elements
        position. It is either *ascending* or *descending* based on the
        ordering combined index.
      type: string
      enum: [ ASCENDING, DESCENDING ]

    query_hash:
      description: >
        Stable hash calculated over all query filters applied to create the
        collection resource that is represented by this cursor.
      type: string

    query:
      description: >
        Object containing all query filters applied to create the collection
        resource that is represented by this cursor.
      type: object
      properties: ...

  required:
    - position
    - element
    - direction
```

`id`\</a\>"\>**Note:** In case of complex and long search requests, e.g.
when `GET with body` is already required, the `cursor` may not be able
to include the `query` because of common HTTP parameter size
restrictions. In this case the `query` filters should be transported via
body - in the request as well as in the response, while the pagination
consistency should be ensured via the `query_hash`.

`id`\</a\>"\>**Remark:** It is also important to check the efficiency of
the data-access. You need to make sure that you have a fully ordered
stable index, that allows to efficiently resolve all elements of a page.
If necessary, you need to provide a combined index that includes the
`id` to ensure the full order and additional filter criteria to ensure
efficiency.

## Further reading

  - [Twitter](https://dev.twitter.com/rest/public/timelines)

  - [Use the Index, Luke](http://use-the-index-luke.com/no-offset)

  - [Paging in
    PostgreSQL](https://www.citusdata.com/blog/1872-joe-nelson/409-five-ways-paginate-postgres-basic-exotic)

# Optimistic locking in RESTful APIs

## Introduction

`id`\</a\>"\>Optimistic locking might be used to avoid concurrent writes
on the same entity, which might cause data loss. A client always has to
retrieve a copy of an entity first and specifically update this one. If
another version has been created in the meantime, the update should
fail. In order to make this work, the client has to provide some kind of
version reference, which is checked by the service, before the update is
executed. Please read the more detailed description on how to update
resources via `PUT` in the [HTTP Requests Section](#put).

`id`\</a\>"\>A RESTful API usually includes some kind of search
endpoint, which will then return a list of result entities. There are
several ways to implement optimistic locking in combination with search
endpoints which, depending on the approach chosen, might lead to
performing additional requests to get the current version of the entity
that should be updated.

## `ETag` with `If-Match` header

`id`\</a\>"\>An `ETag` can only be obtained by performing a `GET`
request on the single entity resource before the update, i.e. when using
a search endpoint an additional request is necessary.

`id`\</a\>"\>Example:

``` http
< GET /orders

> HTTP/1.1 200 OK
> {
>   "items": [
>     { "id": "O0000042" },
>     { "id": "O0000043" }
>   ]
> }

< GET /orders/BO0000042

> HTTP/1.1 200 OK
> ETag: osjnfkjbnkq3jlnksjnvkjlsbf
> { "id": "BO0000042", ... }

< PUT /orders/O0000042
< If-Match: osjnfkjbnkq3jlnksjnvkjlsbf
< { "id": "O0000042", ... }

> HTTP/1.1 204 No Content
```

`id`\</a\>"\>Or, if there was an update since the `GET` and the entity’s
`ETag` has changed:

``` http
> HTTP/1.1 412 Precondition failed
```

### Pros

  - RESTful solution

### Cons

  - Many additional requests are necessary to build a meaningful
    front-end

## `ETags` in result entities

`id`\</a\>"\>The ETag for every entity is returned as an additional
property of that entity. In a response containing multiple entities,
every entity will then have a distinct `ETag` that can be used in
subsequent `PUT` requests.

`id`\</a\>"\>In this solution, the `etag` property should be `readonly`
and never be expected in the `PUT` request payload.

`id`\</a\>"\>Example:

``` http
< GET /orders

> HTTP/1.1 200 OK
> {
>   "items": [
>     { "id": "O0000042", "etag": "osjnfkjbnkq3jlnksjnvkjlsbf", "foo": 42, "bar": true },
>     { "id": "O0000043", "etag": "kjshdfknjqlowjdsljdnfkjbkn", "foo": 24, "bar": false }
>   ]
> }

< PUT /orders/O0000042
< If-Match: osjnfkjbnkq3jlnksjnvkjlsbf
< { "id": "O0000042", "foo": 43, "bar": true }

> HTTP/1.1 204 No Content
```

`id`\</a\>"\>Or, if there was an update since the `GET` and the entity’s
`ETag` has changed:

``` http
> HTTP/1.1 412 Precondition failed
```

### Pros

  - Perfect optimistic locking

### Cons

  - Information that only belongs in the HTTP header is part of the
    business objects

## Version numbers

`id`\</a\>"\>The entities contain a property with a version number. When
an update is performed, this version number is given back to the service
as part of the payload. The service performs a check on that version
number to make sure it was not incremented since the consumer got the
resource and performs the update, incrementing the version number.

`id`\</a\>"\>Since this operation implies a modification of the resource
by the service, a `POST` operation on the exact resource (e.g. `POST
/orders/O0000042`) should be used instead of a `PUT`.

`id`\</a\>"\>In this solution, the `version` property is not `readonly`
since it is provided at `POST` time as part of the payload.

`id`\</a\>"\>Example:

``` http
< GET /orders

> HTTP/1.1 200 OK
> {
>   "items": [
>     { "id": "O0000042", "version": 1,  "foo": 42, "bar": true },
>     { "id": "O0000043", "version": 42, "foo": 24, "bar": false }
>   ]
> }

< POST /orders/O0000042
< { "id": "O0000042", "version": 1, "foo": 43, "bar": true }

> HTTP/1.1 204 No Content
```

`id`\</a\>"\>or if there was an update since the `GET` and the version
number in the database is higher than the one given in the request body:

``` http
> HTTP/1.1 409 Conflict
```

### Pros

  - Perfect optimistic locking

### Cons

  - Functionality that belongs into the HTTP header becomes part of the
    business object

  - Using `POST` instead of PUT for an update logic (not a problem in
    itself, but may feel unusual for the consumer)

## `Last-Modified` / `If-Unmodified-Since`

`id`\</a\>"\>In HTTP 1.0 there was no `ETag` and the mechanism used for
optimistic locking was based on a date. This is still part of the HTTP
protocol and can be used. Every response contains a `Last-Modified`
header with a HTTP date. When requesting an update using a `PUT`
request, the client has to provide this value via the header
`If-Unmodified-Since`. The server rejects the request, if the last
modified date of the entity is after the given date in the header.

`id`\</a\>"\>This effectively catches any situations where a change that
happened between `GET` and `PUT` would be overwritten. In the case of
multiple result entities, the `Last-Modified` header will be set to the
latest date of all the entities. This ensures that any change to any of
the entities that happens between `GET` and `PUT` will be detectable,
without locking the rest of the batch as well.

`id`\</a\>"\>Example:

``` http
< GET /orders

> HTTP/1.1 200 OK
> Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
> {
>   "items": [
>     { "id": "O0000042", ... },
>     { "id": "O0000043", ... }
>   ]
> }

< PUT /block/O0000042
< If-Unmodified-Since: Wed, 22 Jul 2009 19:15:56 GMT
< { "id": "O0000042", ... }

> HTTP/1.1 204 No Content
```

`id`\</a\>"\>Or, if there was an update since the `GET` and the entities
last modified is later than the given date:

``` http
> HTTP/1.1 412 Precondition failed
```

### Pros

  - Well established approach that has been working for a long time

  - No interference with the business objects; the locking is done via
    HTTP headers only

  - Very easy to implement

  - No additional request needed when updating an entity of a search
    endpoint result

### Cons

  - If a client communicates with two different instances and their
    clocks are not perfectly in sync, the locking could potentially fail

## Conclusion

`id`\</a\>"\>We suggest to either use the *`ETag` in result entities* or
*`Last-Modified` / `If-Unmodified-Since`* approach.

# Changelog

`id`\</a\>"\>Non-major changes are editorial-only changes or minor
changes of existing guidelines, e.g. adding new error code. Major
changes are changes that come with additional obligations, or even
change an existing guideline obligation. The latter changes are
additionally labeled with "Rule Change" here.

`id`\</a\>"\>(Note that recent changes might be missing, as we update
this list only occasionally, not with each pull request, to avoid merge
commits.)

# Rule Changes

  - `2021-05-14:` Introduced the changelog. From now on all rule changes
    on API guidelines will be recorded here.

var ruleIdRegEx = /(\\d)+/; var h3headers =
document.getElementsByTagName("h3"); for (var i = 0; i

script\>

var toc = document.getElementById('toc'); var div =
document.createElement('div'); div.id = 'table-of-contents';
toc.parentNode.replaceChild(div, toc); div.appendChild(toc); var ul =
toc.childNodes\[3\]; ul.removeChild(ul.childNodes\[1\]);

var header = document.getElementById('header'); var nav =
document.createElement('div'); nav.id = 'toc';
nav.classList.add('toc2'); var title = document.createElement('div');
title.id = 'toctitle'; var link = document.createElement('a');
link.innerText = 'API Guidelines'; link.href = '\#'; title.append(link);
nav.append(title); var ul = document.createElement('ul');
ul.classList.add('sectlevel1'); var link = document.createElement('a');
link.innerHTML = 'Table of Contents'; link.href = '\#table-of-contents';
li = document.createElement('li'); li.append(link); ul.append(li); var
link, li; var h2headers = document.getElementsByTagName('h2'); for (var
i = 1; i

script\>

1.  Per definition of R.Fielding REST APIs have to support HATEOAS
    (maturity level 3). Our guidelines do not strongly advocate for full
    REST compliance, but limited hypermedia usage, e.g. for pagination
    (see [Hypermedia](#hypermedia)). However, we still use the term
    "RESTful API", due to the absence of an alternative established term
    and to keep it like the very majority of web service industry that
    also use the term for their REST approximations — in fact, in
    today’s industry full HATEOAS compliant APIs are a very rare
    exception.

2.  HTTP/1.1 standard
    ([RFC 7230](https://tools.ietf.org/html/rfc7230#section-6.1))
    defines two types of headers: end-to-end and hop-by-hop headers.
    End-to-end headers must be transmitted to the ultimate recipient of
    a request or response. Hop-by-hop headers, on the contrary, are
    meaningful for a single connection only.

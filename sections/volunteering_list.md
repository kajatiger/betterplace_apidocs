
# Volunteering List ⇄ [Details](volunteering_details.md)

```Rebol
GET https://api.betterplace.org/de/api_v4/volunteering.json?around=10997+Berlin%2C+Germany&around_distance=25km&nelat=51.123&nelng=12.123&order=content_updated_at%3AASC&q=Homework+help&scope=location&swlat=51.001&swlng=12.001
```

A list of betterplace.org volunteering offers (donate time).
Results are contained in a *data* attribute.

**For [betterplace.org clients](../README.md#client-api):**
This resource is not avaliable at the moment.


## URL Parameters

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <th align="left">scope</th>
    <td><code>location</code></td>
    <td>no</td>
    <td>Use the scope to specify how the search-query <code>q</code> should behave:
<ul>
<li>"no scope" (default) performs a full text search
<li><code>human_name</code> searches only on the manager-fullname and carrier-fullname.
  Use this to get all entities by "Unicef" or by "Till Behnke".
<li><code>location</code> does a reverse geocoding lookup.
  This lookup returns a bounding-box. We transform this bounding-box in a
  rectangle that is large enough to encapsulate the whole bounding-box.
  We then return all entities that belong to this rectangle.
</ul>
<a href="../README.md#request-parameter-format">Learn how to format the parameter</a>.
</td>
  </tr>
  <tr>
    <th align="left">around</th>
    <td><code>10997 Berlin, Germany</code></td>
    <td>no</td>
    <td>Order the results by the distance to the given location from near to far.
<br>
Location can be provided as …
<br>
<em>… Lat/Lng:</em> <code>52.50,13.45</code>
<br>
<em>… ZIP:</em> <code>10997 Berlin, Germany</code>.
We use the centre of the ZIP code area as center for the search.
Please add enough context information (like the Country name)
so google knows what place you are looking for.
<br>
<em>… any location search:</em> All queries other than a float tuple
are send to the google location service. For the provided response we
take a fitting lat/lng value as center of the search. So in theory,
you can use any search that works for google maps.
<br>
Check the <code>around_location</code> to see what latitude/longitude
values have been used for the query.
</td>
  </tr>
  <tr>
    <th align="left">around_distance</th>
    <td><code>25km</code></td>
    <td>no</td>
    <td>In combination with the <code>around</code> parameter the search will be
limited to results whose location is closer than the given value to the
location provided through the <code>around</code> parameter. Possible
values are all integer values followed by <code>m</code> for meters or
<code>km</code> for kilometers, e.g. <code>1000m</code>, <code>1km</code>.
<br>
When <code>around_distance</code> is given without <code>around</code> it
will be ignored.
</td>
  </tr>
  <tr>
    <th align="left">nelat</th>
    <td><code>51.123</code></td>
    <td>no</td>
    <td>For geographic bound filterning: The northeast corner's latitude.</td>
  </tr>
  <tr>
    <th align="left">nelng</th>
    <td><code>12.123</code></td>
    <td>no</td>
    <td>For geographic bound filterning: The northeast corner's longitude.</td>
  </tr>
  <tr>
    <th align="left">swlat</th>
    <td><code>51.001</code></td>
    <td>no</td>
    <td>For geographic bound filterning: The southwest corner's latitude.</td>
  </tr>
  <tr>
    <th align="left">swlng</th>
    <td><code>12.001</code></td>
    <td>no</td>
    <td>For geographic bound filterning: The southwest corner's longitude.</td>
  </tr>
  <tr>
    <th align="left">q</th>
    <td><code>Homework help</code></td>
    <td>no</td>
    <td>Search query. The searches behaviour is based on the scope.</td>
  </tr>
  <tr>
    <th align="left">order</th>
    <td><code>content_updated_at:ASC</code></td>
    <td>no</td>
    <td>Order the result by <code>has_image</code> (default),
<code>content_updated_at</code> (second default). Use the optional
<code>ASC</code> (default) or <code>DESC</code>.
<a href="../README.md#request-parameter-format">Learn how to format the parameter</a>.
<br>
The default order is the same as for the
<a href="http://www.betterplace.org/en/volunteering/list">betterplace.org volunteering list</a>:
<code>has_image:desc| carrier_has_image:desc| content_updated_at:desc</code>
</td>
  </tr>
</table>


## Response Attributes

### Root Attributes

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">id</th>
      <td>number</td>
      <td>1</td>
      <td>An integer number ≥ 1</td>
    </tr>
    <tr>
      <th align="left">created_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">updated_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">latitude</th>
      <td>number</td>
      <td>52.499007</td>
      <td>Decimal degrees based on user input</td>
    </tr>
    <tr>
      <th align="left">longitude</th>
      <td>number</td>
      <td>13.44947</td>
      <td>Decimal degrees based on user input</td>
    </tr>
    <tr>
      <th align="left">street</th>
      <td>null &#124; string</td>
      <td>"Schlesische Straße 26"</td>
      <td>Street address</td>
    </tr>
    <tr>
      <th align="left">zip</th>
      <td>null &#124; string</td>
      <td>"10997"</td>
      <td>ZIP code</td>
    </tr>
    <tr>
      <th align="left">city</th>
      <td>null &#124; string</td>
      <td>"Berlin"</td>
      <td>Name of the city</td>
    </tr>
    <tr>
      <th align="left">country</th>
      <td>null &#124; string</td>
      <td>"Deutschland"</td>
      <td>Name of the country</td>
    </tr>
    <tr>
      <th align="left">content_updated_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">title</th>
      <td>string</td>
      <td>TODO</td>
      <td>Max 100 character unless the volunteering is imported</td>
    </tr>
    <tr>
      <th align="left">description</th>
      <td>string</td>
      <td></td>
      <td>A description of the offer. This may contain any of the following
HTML tags: <code>br, strong, b, em, i, ul, ol, li, p</code>.
</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="carrier-ref" href="#carrier">
            ↓carrier
          </a>
        </th>
      <td>object</td>
      <td>TODO</td>
      <td>An organisation, Users will be added later</td>
    </tr>
    <tr>
      <th align="left">vacancies</th>
      <td>number</td>
      <td>1</td>
      <td>The number of volunteers that are needed, provided by the manager</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="image-ref" href="#image">
            ↓image
          </a>
        </th>
      <td>null &#124; object</td>
      <td>TODO</td>
      <td>Each volunteering has one optional image / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="contact-ref" href="#contact">
            ↓contact
          </a>
        </th>
      <td>object</td>
      <td>TODO</td>
      <td>Contact person, contact data and contact address</td>
    </tr>
    <tr>
      <th align="left">location_fixed</th>
      <td>boolean</td>
      <td>true</td>
      <td>Specifies whether the volunteering offer is limited to a certain location or if it may be
executed remotely.
</td>
    </tr>
    <tr>
      <th align="left">working_time_selection</th>
      <td>string</td>
      <td>regular commitment</td>
      <td>Working time selection, specifies if this is a one-time event or if
this volunteering can takes place regulary.
</td>
    </tr>
    <tr>
      <th align="left">working_time_weekends</th>
      <td>array</td>
      <td>["in the mornings"]</td>
      <td>Up to three working time preferences. They specify when this volunteering
should take place on weekends.
</td>
    </tr>
    <tr>
      <th align="left">working_time_weekdays</th>
      <td>array</td>
      <td>["in the mornings"]</td>
      <td>Up to three working time preferences. They specify when this volunteering
should take place on weekdays.
</td>
    </tr>
    <tr>
      <th align="left">begins_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">ends_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">topics</th>
      <td>array</td>
      <td>["Development cooperation", "Children & youth"]</td>
      <td>Up to 4 categories that describe, what for which causes you need volunteers.
Results are translated to the requested language.
Possible results: "Animal & environment protection", "Culture & sports",
"Children & youth", "Development cooperation ", "DisabledEducation", "Elderly people",
"Human rights", "Refugees & immigrants", "Invalid", "Local help", "Socially deprived"
</td>
    </tr>
    <tr>
      <th align="left">activities</th>
      <td>array &#124; null</td>
      <td>["consulting/coaching", "office work"]</td>
      <td>Up to 4 categories that describe, what for which causes you need volunteers.
Results are translated to the requested language.
Possible results: "consulting/coaching", "crafting/gardening", "doing sports",
"doing the chores", "group care", "nursing/parenting", "office work",
"organising/managing", "painting/designing", "tutoring/reading",
"visiting/accompanying", "writing/translating"
</td>
    </tr>
    <tr>
      <th align="left">imported_from</th>
      <td>null &#124; string</td>
      <td>aktion_mensch</td>
      <td>Betterplace imports volunteering offers from Aktions Mensch.</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="import_information-ref" href="#import_information">
            ↓import_information
          </a>
        </th>
      <td>null &#124; object</td>
      <td>TODO</td>
      <td>Meta data concerning the import of this volunteering offer, if it
was indeed imported.
</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="profile_picture-ref" href="#profile_picture">
            ↓profile_picture
          </a>
        </th>
      <td>null &#124; object</td>
      <td></td>
      <td>TODO</td>
    </tr>
  </table>
### <a id="carrier" href="#carrier-ref">↑Nested Attributes: carrier</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">carrier.latitude</th>
      <td>number</td>
      <td>52.499007</td>
      <td>Decimal degrees based on user input</td>
    </tr>
    <tr>
      <th align="left">carrier.longitude</th>
      <td>number</td>
      <td>13.44947</td>
      <td>Decimal degrees based on user input</td>
    </tr>
    <tr>
      <th align="left">carrier.name</th>
      <td>string</td>
      <td>"Viva con Agua de Sankt Pauli e.V."</td>
      <td>An organisation name, Users will be added later</td>
    </tr>
    <tr>
      <th align="left">carrier.street</th>
      <td>string</td>
      <td>"Rosenstr. 3"</td>
      <td>Contact data for the organisation</td>
    </tr>
    <tr>
      <th align="left">carrier.city</th>
      <td>string</td>
      <td>"Berlin"</td>
      <td>Contact data for the organisation</td>
    </tr>
    <tr>
      <th align="left">carrier.zip</th>
      <td>string</td>
      <td>"10123"</td>
      <td>Contact data for the organisation</td>
    </tr>
    <tr>
      <th align="left">carrier.country</th>
      <td>string</td>
      <td>"Germany"</td>
      <td>Contact data for the organisation</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="carrier.picture-ref" href="#carrier.picture">
            ↓carrier.picture
          </a>
        </th>
      <td>null &#124; object</td>
      <td></td>
      <td>TODO</td>
    </tr>
  </table>
### <a id="carrier.picture" href="#carrier.picture-ref">↑Nested Attributes: carrier.picture</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">carrier.picture.fallback</th>
      <td>boolean</td>
      <td>true</td>
      <td>Specifies whether a fallback image is given or not</td>
    </tr>
  </table>
### <a id="image" href="#image-ref">↑Nested Attributes: image</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">image.description</th>
      <td>string</td>
      <td></td>
      <td>Image description</td>
    </tr>
  </table>
### <a id="contact" href="#contact-ref">↑Nested Attributes: contact</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">contact.name</th>
      <td>string</td>
      <td>Till Behnke</td>
      <td>Fullname of the contact person.
For imported volunteering offers, this is the
contact-name that is provided on import.
</td>
    </tr>
    <tr>
      <th align="left">contact.phone</th>
      <td>string</td>
      <td>030 - 7676 4488 44</td>
      <td>Phone number for direct contact.
No validations on input apply.
</td>
    </tr>
    <tr>
      <th align="left">contact.email</th>
      <td>string</td>
      <td>support@betterplace.org</td>
      <td>Plain text email-address for direct contact
</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="contact.picture-ref" href="#contact.picture">
            ↓contact.picture
          </a>
        </th>
      <td>object</td>
      <td>//assets.betterplace.org/…</td>
      <td>User profile picture or a fallback image</td>
    </tr>
  </table>
### <a id="contact.picture" href="#contact.picture-ref">↑Nested Attributes: contact.picture</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">contact.picture.fallback</th>
      <td>boolean</td>
      <td>true</td>
      <td>Specifies whether a fallback image is given or not</td>
    </tr>
  </table>
### <a id="import_information" href="#import_information-ref">↑Nested Attributes: import_information</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">import_information.created_at</th>
      <td>null &#124; string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone) when the imported record was actually created.
</td>
    </tr>
    <tr>
      <th align="left">import_information.updated_at</th>
      <td>null &#124; string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone) when the imported record was
actually updated last.
</td>
    </tr>
    <tr>
      <th align="left">import_information.import_type</th>
      <td>string</td>
      <td>"Import::ImportFormat"</td>
      <td>Type of import this record originated from.</td>
    </tr>
    <tr>
      <th align="left">import_information.import_id</th>
      <td>string</td>
      <td>"foo:23"</td>
      <td>Unique identifier for this imported record.
</td>
    </tr>
    <tr>
      <th align="left">import_information.imported_at</th>
      <td>string</td>
      <td>"1994-11-15T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone) when the record was imported at
betterplace.
</td>
    </tr>
  </table>
### <a id="profile_picture" href="#profile_picture-ref">↑Nested Attributes: profile_picture</a>

  <table>
    <tr>
      <th>Attribute</th>
      <th>Types</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
    <tr>
      <th align="left">profile_picture.fallback</th>
      <td>boolean</td>
      <td>true</td>
      <td>Specifies whether a fallback image is given or not</td>
    </tr>
  </table>
</table>

## Response Links

<table>
  <tr>
    <th>Linkname</th>
    <th>Description</th>
  </tr>

    <tr>
      <th align="left">self</th>
      <td>Link to this resource itself
(<a href="volunteering_details.md">volunteering details</a>)
</td>
    </tr>
    <tr>
      <th align="left">platform</th>
      <td>Permalink to betterplace.org</td>
    </tr>
    <tr>
      <th align="left">inquiries</th>
      <td>The URL to which inquiries about this offer can be POSTed
(<a href="volunteering_inquiries.md">inquiry details</a>).
Templated, needs insertion of the client_id.
</td>
    </tr>
    <tr>
      <th align="left">carrier.self</th>
      <td>Link to this resource itself
(<a href="organisation_details.md">organisation details</a>)
</td>
    </tr>
    <tr>
      <th align="left">carrier.picture.fill_100x100</th>
      <td>100×100 Pixel</td>
    </tr>
    <tr>
      <th align="left">carrier.picture.fill_200x200</th>
      <td>200×200 Pixel</td>
    </tr>
    <tr>
      <th align="left">carrier.picture.fill_400x400</th>
      <td>400×400 Pixel</td>
    </tr>
    <tr>
      <th align="left">carrier.picture.original</th>
      <td>Maximum sized image. This is the original image with default-cropping or user-cropping applied.</td>
    </tr>
    <tr>
      <th align="left">image.fill_618x322</th>
      <td>618×322 Pixel / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">image.fill_270x141</th>
      <td>270×141 Pixel / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">image.original</th>
      <td>Original size / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">image.thumb</th>
      <td>Thumbnail size / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">image.medium</th>
      <td>Medium size / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">image.regular</th>
      <td>Regular size / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">contact.picture.fill_100x100</th>
      <td>100×100 Pixel</td>
    </tr>
    <tr>
      <th align="left">contact.picture.original</th>
      <td>Maximum sized image. This is the original image with default-cropping or user-cropping applied.</td>
    </tr>
    <tr>
      <th align="left">profile_picture.fill_960x500</th>
      <td>950×500 Pixel</td>
    </tr>
    <tr>
      <th align="left">profile_picture.fill_730x380</th>
      <td>730×380 Pixel</td>
    </tr>
    <tr>
      <th align="left">profile_picture.fill_618x322</th>
      <td>618×322 Pixel / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">profile_picture.fill_410x214</th>
      <td>410×214 Pixel</td>
    </tr>
    <tr>
      <th align="left">profile_picture.fill_270x141</th>
      <td>270×141 Pixel / DEPRECATED, will be removed after 5/2015</td>
    </tr>
    <tr>
      <th align="left">profile_picture.original</th>
      <td>Maximum sized image. This is the original image with default-cropping or user-cropping applied.</td>
    </tr>
</table>

## Response Example

```json
{
  "total_entries": 5922,
  "offset": 3,
  "total_pages": 1974,
  "current_page": 2,
  "per_page": 3,
  "data": [
    {
      "id": 6778,
      "created_at": "2013-02-11T12:40:07+01:00",
      "updated_at": "2016-01-04T11:23:29+01:00",
      "latitude": 48.7754,
      "longitude": 9.18176,
      "street": "",
      "zip": "",
      "city": "Stuttgart",
      "country": "Deutschland",
      "content_updated_at": "2016-01-04T11:23:29+01:00",
      "title": "Ehrenamtliche Helfer",
      "description": "Wir suchen für unseren Verein ehrenamtliche Helfer, die Lust haben, Projekte für und mit Kindern und Jugendlichen zu unterstützen oder selbst durchzuführen. Gerne darfst du auch eigene Ideen und Projekte mitbringen, die wir gemeinsam verwirklichen.<br>Informationen über uns findest du unter www.choice-germany.com. Wir freuen uns sehr dich bald in unserem Team begrüßen zu dürfen ;)",
      "carrier": {
        "latitude": 48.76653,
        "longitude": 9.26905999999997,
        "name": "choice e.V.",
        "street": "Mirabellenstraße 28",
        "city": "Stuttgart",
        "zip": "70329",
        "country": "Deutschland",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/007/375/fill_100x100_profile_thumb_110206_Logo_Bild_kl_-_Cr_Xo_Kopie.png"
            },
            {
              "rel": "fill_200x200",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/007/375/fill_200x200_profile_thumb_110206_Logo_Bild_kl_-_Cr_Xo_Kopie.png"
            },
            {
              "rel": "fill_400x400",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/007/375/fill_400x400_profile_thumb_110206_Logo_Bild_kl_-_Cr_Xo_Kopie.png"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/007/375/crop_original_profile_thumb_110206_Logo_Bild_kl_-_Cr_Xo_Kopie.png"
            }
          ]
        },
        "links": [
          {
            "rel": "self",
            "href": "https://api.betterplace.org/de/api_v4/organisations/7375.json"
          }
        ]
      },
      "vacancies": 5,
      "image": {
        "description": "Unser choice-Team",
        "links": [
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_618x322_Team.jpg"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_270x141_Team.jpg"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/Team.jpg"
          },
          {
            "rel": "thumb",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/thumb_Team.jpg"
          },
          {
            "rel": "medium",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/medium_Team.jpg"
          },
          {
            "rel": "regular",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/regular_Team.jpg"
          }
        ]
      },
      "contact": {
        "name": "Ralf Müller",
        "phone": "",
        "email": "stuttgart@choice-germany.com",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/185/514/fill_100x100_choice-Webseite.png"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/185/514/crop_original_choice-Webseite.png"
            }
          ]
        },
        "links": [

        ]
      },
      "location_fixed": true,
      "working_time_selection": "egal wann / nach Vereinbarung",
      "working_time_weekends": [

      ],
      "working_time_weekdays": [

      ],
      "begins_at": null,
      "ends_at": null,
      "topics": [
        "Bildung",
        "Entwicklungszusammenarbeit",
        "Kinder & Jugendliche",
        "Sozial Benachteiligte"
      ],
      "activities": [
        "organisieren/planen"
      ],
      "imported_from": null,
      "import_information": null,
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_960x500_Team.jpg"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_730x380_Team.jpg"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_618x322_Team.jpg"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_410x214_Team.jpg"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/fill_270x141_Team.jpg"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/778/crop_original_Team.jpg"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/volunteering/6778.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/volunteering/6778-ehrenamtliche-helfer"
        },
        {
          "rel": "inquiries",
          "href": "https://api.betterplace.org/de/api_v4/clients/%7Bclient_id%7D/volunteering/6778-ehrenamtliche-helfer/inquiries.json",
          "templated": true
        }
      ]
    },
    {
      "id": 6801,
      "created_at": "2013-02-12T12:58:15+01:00",
      "updated_at": "2016-02-23T13:22:58+01:00",
      "latitude": 53.5511,
      "longitude": 9.99368,
      "street": "",
      "zip": "",
      "city": "Hamburg",
      "country": "Deutschland",
      "content_updated_at": "2016-02-23T13:22:58+01:00",
      "title": "Als Mentor/in bei Kindern die Lust am Lesen wecken",
      "description": "Unsere ehrenamtlichen Mentoren sind Leselernhelfer. Mit Nachhilfe oder Förderunterricht hat dies nichts zu tun. Mentoren wissen, wie wertvoll Bücher und Bildung sind. Und dass man Lesen fürs Leben lernt, nicht nur für die Schule. Ihr Wissen und ihre Begeisterung geben die Mentoren weiter an Schülerinnen und Schüler, die sich mit Sprache schwer tun.<br><br>Wir suchen Menschen, die:<br>    - selbst Freude am Lesen haben<br>    - geduldig, freundlich und respektvoll mit Kindern umgehen<br>    - Spaß am Gespräch und auch am Zuhören haben<br>    - Menschen aus anderen Kulturen vorurteilsfrei begegnen<br>    - zuverlässig sind<br><br>Einmal wöchentlich treffen sich Mentor und Lesekind für circa eine Stunde in der Schule zur gemeinsamen Lesestunde. Ihre Tätigkeit soll nicht den Deutschunterricht ersetzen und ist auch nicht als Nachhilfe gedacht. Das Lesekind soll keinen Leistungsdruck erleben, sondern mit Freude an die Bücher herangeführt werden. <br><br>MENTOR HAMBURG e.V. bietet den Mentoren:<br>    - eine sorgfältige Vorbereitung für ihre Mentortätigkeit<br>    - eine Vermittlung mit einem Lesekind an einer wohnortsnahen Schule<br>    - regelmäßige Mentorentreffen zum kollegialen Austausch<br>    - vielfältige Weiterbildungsangebote über das ganze Jahr<br>    - Bücherlisten, Lesetipps und Ideen, wie die Lesestunden gestaltet werden könnten<br>    - einmal im Jahr die Möglichkeit gemeinsam mit dem Lesekind ins Theater zu gehen<br>    - die Möglichkeit, kostenlos mit dem Lesekind ins Kinderbuchhaus oder Schulmuseum zu gehen",
      "carrier": {
        "latitude": 53.549379,
        "longitude": 10.008464,
        "name": "MENTOR - Die Leselernhelfer HAMBURG e.V.",
        "street": "Hühnerposten 1 C",
        "city": "Hamburg",
        "zip": "20539",
        "country": "Deutschland",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/013/116/fill_100x100_1_MENTOR_Jubilaeumslogo_RZ1_CMYK-trans.jpg"
            },
            {
              "rel": "fill_200x200",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/013/116/fill_200x200_1_MENTOR_Jubilaeumslogo_RZ1_CMYK-trans.jpg"
            },
            {
              "rel": "fill_400x400",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/013/116/fill_400x400_1_MENTOR_Jubilaeumslogo_RZ1_CMYK-trans.jpg"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/013/116/crop_original_1_MENTOR_Jubilaeumslogo_RZ1_CMYK-trans.jpg"
            }
          ]
        },
        "links": [
          {
            "rel": "self",
            "href": "https://api.betterplace.org/de/api_v4/organisations/13116.json"
          }
        ]
      },
      "vacancies": 20,
      "image": {
        "description": "",
        "links": [
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_618x322_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_270x141_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/Foto-MENTOR-2.jpg"
          },
          {
            "rel": "thumb",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/thumb_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "medium",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/medium_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "regular",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/regular_Foto-MENTOR-2.jpg"
          }
        ]
      },
      "contact": {
        "name": "Sandra Weis",
        "phone": "",
        "email": "info@mentor-hamburg.de",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/294/993/fill_100x100_original_MENTOR_HH_Logo.jpg"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/294/993/crop_original_original_MENTOR_HH_Logo.jpg"
            }
          ]
        },
        "links": [

        ]
      },
      "location_fixed": true,
      "working_time_selection": "egal wann / nach Vereinbarung",
      "working_time_weekends": [

      ],
      "working_time_weekdays": [

      ],
      "begins_at": null,
      "ends_at": null,
      "topics": [
        "Bildung",
        "Kinder & Jugendliche",
        "Flüchtlinge & Migranten",
        "Sozial Benachteiligte"
      ],
      "activities": [
        "beraten/coachen",
        "besuchen/begleiten",
        "Nachhilfe/vorlesen"
      ],
      "imported_from": null,
      "import_information": null,
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_960x500_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_730x380_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_618x322_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_410x214_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/fill_270x141_Foto-MENTOR-2.jpg"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/bettertime/job_description/profile_picture/000/006/801/crop_original_Foto-MENTOR-2.jpg"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/volunteering/6801.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/volunteering/6801-als-mentor-in-bei-kindern-die-lust-am-lesen-wecken"
        },
        {
          "rel": "inquiries",
          "href": "https://api.betterplace.org/de/api_v4/clients/%7Bclient_id%7D/volunteering/6801-als-mentor-in-bei-kindern-die-lust-am-lesen-wecken/inquiries.json",
          "templated": true
        }
      ]
    },
    {
      "id": 6831,
      "created_at": "2013-02-13T18:44:17+01:00",
      "updated_at": "2016-03-01T12:38:46+01:00",
      "latitude": 0.1893,
      "longitude": 34.9484,
      "street": "57726",
      "zip": "",
      "city": "Kisumu",
      "country": "Kenia",
      "content_updated_at": "2016-03-01T12:38:46+01:00",
      "title": "experience the diverse village stories and mythologies",
      "description": "Teaching and instructing young children to read and write",
      "carrier": {
        "latitude": -0.15000000596046,
        "longitude": 35.20000076293945,
        "name": "Center For People Development",
        "street": "Akodhe Loth road",
        "city": "Kisumu",
        "zip": "40107",
        "country": "Kenia",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/004/629/fill_100x100_profile_thumb_LOGO_2.png"
            },
            {
              "rel": "fill_200x200",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/004/629/fill_200x200_profile_thumb_LOGO_2.png"
            },
            {
              "rel": "fill_400x400",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/004/629/fill_400x400_profile_thumb_LOGO_2.png"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/organisation/profile_picture/000/004/629/crop_original_profile_thumb_LOGO_2.png"
            }
          ]
        },
        "links": [
          {
            "rel": "self",
            "href": "https://api.betterplace.org/de/api_v4/organisations/4629.json"
          }
        ]
      },
      "vacancies": 2,
      "image": {
        "description": "",
        "links": [
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_618x322_default.betterplace.png"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_270x141_default.betterplace.png"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_730x380_default.betterplace.png"
          },
          {
            "rel": "thumb",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/thumb_default.betterplace.png"
          },
          {
            "rel": "medium",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/medium_default.betterplace.png"
          },
          {
            "rel": "regular",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/regular_default.betterplace.png"
          }
        ]
      },
      "contact": {
        "name": "PETER OTIENO",
        "phone": "+254722261101",
        "email": "khayombe@gmail.com",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/127/272/fill_100x100_peter_o320140319-23207-8rvpxr.jpg"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/127/272/crop_original_peter_o320140319-23207-8rvpxr.jpg"
            }
          ]
        },
        "links": [

        ]
      },
      "location_fixed": true,
      "working_time_selection": "egal wann / nach Vereinbarung",
      "working_time_weekends": [

      ],
      "working_time_weekdays": [

      ],
      "begins_at": null,
      "ends_at": null,
      "topics": [
        "Bildung",
        "Kinder & Jugendliche"
      ],
      "activities": [
        "Nachhilfe/vorlesen"
      ],
      "imported_from": null,
      "import_information": null,
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_960x500_default.betterplace.png"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_730x380_default.betterplace.png"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_618x322_default.betterplace.png"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_410x214_default.betterplace.png"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/fill_270x141_default.betterplace.png"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/assets/default/job_description_profile_picture/crop_original_default.betterplace.png"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/volunteering/6831.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/volunteering/6831-experience-the-diverse-village-stories-and-mythologies"
        },
        {
          "rel": "inquiries",
          "href": "https://api.betterplace.org/de/api_v4/clients/%7Bclient_id%7D/volunteering/6831-experience-the-diverse-village-stories-and-mythologies/inquiries.json",
          "templated": true
        }
      ]
    }
  ]
}
```


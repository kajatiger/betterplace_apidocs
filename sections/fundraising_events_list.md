
# Fundraising Event List ⇄ [Details](fundraising_event_details.md)

```Rebol
GET https://api.betterplace.org/de/api_v4/fundraising_events.json?facets=tax_deductible%3Atrue&order=rank%3ADESC&q=Die+Eckerts&scope=location
```

A list of betterplace.org fundraising events (donate money).
Results are contained in a *data* attribute.

**For [betterplace.org clients](../README.md#client-api):**
Use this resource like `/clients/PERMALINK/fundraising-events.json`


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
</ul>
<a href="../README.md#request-parameter-format">Learn how to format the parameter</a>.
</td>
  </tr>
  <tr>
    <th align="left">q</th>
    <td><code>Die Eckerts</code></td>
    <td>no</td>
    <td>Search query. The searches behaviour is based on the scope.</td>
  </tr>
  <tr>
    <th align="left">facets</th>
    <td><code>tax_deductible:true</code></td>
    <td>no</td>
    <td>Filter the result set.
Documented and supported filters are:
<ul>
<li><code>tax_deductible:true/false</code>
<li><code>prohibit_donations:true/false</code>
</ul>
It is possible to set multiple facet filters.
<a href="../README.md#request-parameter-format">Learn how to format the parameter</a>.
</td>
  </tr>
  <tr>
    <th align="left">order</th>
    <td><code>rank:DESC</code></td>
    <td>no</td>
    <td>Order the results by <code>score</code> (only when a query (q) is given),
<code>rank</code>, <code>id</code>, <code>progress_percentage</code>,
<code>tax_deductible</code>, <code>created_at</code>, <code>updated_at</code>,
<code>last_donation_at</code>, <code>completed</code>.
Use the optional <code>ASC</code> (default) or <code>DESC</code>.
<a href="../README.md#request-parameter-format">Learn how to format the parameter</a>.
<br>
The default order is the same as for the
<a href="https://www.betterplace.org/en/projects/list?search_form%5Bfilters%5D%5Btype%5D=Group">betterplace.org fundraising events list</a>:
<code>completed:asc| score:desc | rank:desc| last_donation_at:desc</code>
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
      <th align="left">content_updated_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone)</td>
    </tr>
    <tr>
      <th align="left">title</th>
      <td>string</td>
      <td>Gemeinsam gegen Ebola: Deine Spende für Westafrika</td>
      <td>Max 50 character</td>
    </tr>
    <tr>
      <th align="left">description</th>
      <td>string</td>
      <td>Lorem ipsum</td>
      <td>Max 25.000 character</td>
    </tr>
    <tr>
      <th align="left">tax_deductible</th>
      <td>boolean</td>
      <td>true</td>
      <td>True if the fundraising event is marked as tax deductible and
can only support tax deductible projects.
If so, users can request a tax-receipt for their donation
that can be used with the german tax authorities.
</td>
    </tr>
    <tr>
      <th align="left">donations_prohibited</th>
      <td>boolean</td>
      <td>false</td>
      <td>True if the fundraising event must not and cannot receive donations.
This might happen if the event was closed by the manager
or blocked by a platform administrator.

Please check this flag whenever you display a donation button.
Should you show a button for an event that cannot receive donations
the user will open the donation form and see an error message on
betterplace.org instead!
</td>
    </tr>
    <tr>
      <th align="left">closed_at</th>
      <td>string</td>
      <td>"1994-11-05T13:15:30Z"</td>
      <td>DateTime (ISO8601 with Timezone) when the fundraising event was closed
by the manager.
</td>
    </tr>
    <tr>
      <th align="left">donor_count</th>
      <td>number</td>
      <td>46</td>
      <td>Number of unique donors, based on the payment-email-address</td>
    </tr>
    <tr>
      <th align="left">donated_amount_in_cents</th>
      <td>number</td>
      <td>232323</td>
      <td>How many cents were already raised with the fundraising event</td>
    </tr>
    <tr>
      <th align="left">requested_amount_in_cents</th>
      <td>number</td>
      <td>12382</td>
      <td>How many cents were requested to be raised with the fundraising event.
This value is optional! The manager decides if his event has a goal or not.
</td>
    </tr>
    <tr>
      <th align="left">progress_percentage</th>
      <td>number</td>
      <td>5</td>
      <td>% financed. This value is only present in case the manager
decided to add a <code>requested_amount_in_cents</code>.
</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="contact-ref" href="#contact">
            ↓contact
          </a>
        </th>
      <td>object</td>
      <td>TODO</td>
      <td>The public face of the fundraising event / fundraising event manager</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="profile_picture-ref" href="#profile_picture">
            ↓profile_picture
          </a>
        </th>
      <td>null &#124; object</td>
      <td>//asset1.betterplace.org ↪/uploads/user/profile_picture ↪/000/000/001 ↪/fill_100x100_original_tb.jpg</td>
      <td>TODO</td>
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
      <th align="left">contact.id</th>
      <td>number</td>
      <td>1</td>
      <td>An integer number ≥ 1</td>
    </tr>
    <tr>
      <th align="left">contact.name</th>
      <td>null &#124; string</td>
      <td>"Till B."</td>
      <td>Display name of a betterplace.org user.
Possible formats: "Till B.", "T. Behnke", "Till Behnke".

In the case of donation-opinions the name might also be
empty/null for anonymous donations for anonymous donations.
</td>
    </tr>
    <tr>
        <th align="left" style="white-space: nowrap">
          <a id="contact.picture-ref" href="#contact.picture">
            ↓contact.picture
          </a>
        </th>
      <td>object</td>
      <td>//asset1.betterplace.org ↪/uploads/user/profile_picture ↪/000/000/001 ↪/fill_100x100_original_tb.jpg</td>
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
(<a href="fundraising_event_details.md">fundraising event details</a>)
</td>
    </tr>
    <tr>
      <th align="left">featured_projects</th>
      <td>A list of <a href="projects_list.md">projects</a> are currently supported by the fundraising event.

Please note, that this project list has no fixed relation to the list of projects that received money by this fundraising event (see <a href="fundraising_events_featured_projects_list.md">Featured Projects List</a>).
A Fundraising event manager can change the list of supported projects at any time; regardless if they received money before.
</td>
    </tr>
    <tr>
      <th align="left">forwardings</th>
      <td>Provides a list of forwarded amounts and their receiving projects.

Each fundraising event can have multiple projects that it supports. The fundraising event manager specifies the amount that is forwarded from the fundraising event to the project.
Please note, that this list of forwarded donations and their corresponding receiving projects is not required to be in sync with the <a href="fundraising_events_featured_projects_list.md">Featured Project List endpoint</a>.
To find out, if all donations of the fundraising event have been forwarded, please sum the amounts provided by this api endpoint and compare it to the donated amount attribute of the fundraising event api endpoint.
</td>
    </tr>
    <tr>
      <th align="left">platform</th>
      <td>Permalink to betterplace.org</td>
    </tr>
    <tr>
      <th align="left">new_client_donation</th>
      <td>Link to the donation form. Templated, needs insertion of the client_id.
</td>
    </tr>
    <tr>
      <th align="left">new_donation</th>
      <td>Link to the regular donation form.
</td>
    </tr>
    <tr>
      <th align="left">contact.platform</th>
      <td>The user's profile on betterplace.org.
To view a user profile you have to be logged in.
This array is empty if the user has no useraccount
with betterplace.org but donated via one of our partner.
</td>
    </tr>
    <tr>
      <th align="left">contact.contact_data</th>
      <td>The user's contact data. Please note that you need to be
<a href="../README.md#client-api">authenticated as a client</a> with matching
access rights in order to see this information.
</td>
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
  "total_entries": 4874,
  "offset": 0,
  "total_pages": 1625,
  "current_page": 1,
  "per_page": 3,
  "data": [
    {
      "id": 3457,
      "created_at": "2010-04-28T17:20:10+02:00",
      "updated_at": "2016-04-29T17:25:26+02:00",
      "content_updated_at": "2016-03-21T10:12:29+01:00",
      "title": "\"Mail raus&Attachment vergessen? 1Euro!\"",
      "description": "Wir alle machen mal Fehler. Sie zu vermeiden lernt man am besten durch eine kleine Strafe - in diesem Fall einer Spende von einem Euro. Also: Alle die Euch eine Mail schicken, in der das Attachment vergessen wurde, müssen von Euch den Link zu diesem Fundraising-Team gemailt kriegen - und dann einen Euro spenden. Damit schön viel Geld für einen guten Zweck zusammen kommt und von betterplace.org zu 100 Prozent weitergeleitet wird. Und damit alle Attachmentvergesser endlich aus ihren unverzeihlichen Fehlern lernen.",
      "tax_deductible": true,
      "donations_prohibited": false,
      "closed_at": null,
      "donor_count": 115,
      "donated_amount_in_cents": 36900,
      "requested_amount_in_cents": null,
      "progress_percentage": null,
      "contact": {
        "id": 6,
        "name": "Moritz E.",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/000/006/fill_100x100_original_eckert.png"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/000/006/crop_original_original_eckert.png"
            }
          ]
        },
        "links": [
          {
            "rel": "platform",
            "href": "https://www.betterplace.org/de/users/moritz_e"
          },
          {
            "rel": "contact_data",
            "href": "https://api.betterplace.org/de/api_v4/users/6/contact_data.json"
          }
        ]
      },
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/fill_960x500_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/fill_730x380_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/fill_618x322_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/fill_410x214_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/fill_270x141_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/003/457/crop_original_original_Bildschirmfoto_2010-04-28_um_17.25.56.png"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/3457.json"
        },
        {
          "rel": "featured_projects",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/3457/featured_projects.json"
        },
        {
          "rel": "forwardings",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/3457/forwardings.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/fundraising-events/3457-mail-raus-attachment-vergessen-1euro"
        },
        {
          "rel": "new_client_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/3457/client_donations/new?client_id=%7Bclient_id%7D",
          "templated": true
        },
        {
          "rel": "new_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/3457/donations/new"
        }
      ]
    },
    {
      "id": 27767,
      "created_at": "2016-04-11T14:58:24+02:00",
      "updated_at": "2016-05-31T23:40:53+02:00",
      "content_updated_at": "2016-05-22T19:25:22+02:00",
      "title": "Christoph, Jona & Liv: Geburtstags-SpendenRap 2016",
      "description": "AAAAAH!! MISSION ACCOMPLISHED :):):):):)<br><br>Yabadabadoooo! This is absolutely, absolutely incredible guys. We just hit our goal of 16.200 euros and now hundreds of kids will have a safe birth and get a real shot in life. HOW AWESOME IS THAT?!?! Well done everybody :))) you amaze me every year anew!<br><br>A moment to celebrate and feel the power that we have to make a difference in this world, bit by bit :) Hugs to all of you! Liv, Jona and Christoph <br><br>PS - in case more comes in, the next 250euros will buy all the medical clothes they need and the 1250 euros after that will allow 20 c-sections for critical cases in one of the hospitals nearby...so I upped the counter to 17.700 euros<br><br>ENGLISH BELOW :)  ----<br><br>Am 24.Februar dieses Jahres geschah ein Wunder: Unsere Tochter Liv wurde geboren.<br><br>Wir hatten das große Glück, dass die Kleine dank der mega guten Betreuung durch Ärzte und Hebammen gesund zur Welt kam.  In vielen Ländern sieht die Realität leider anders aus: Die Kleinen sterben bereits bei der Geburt oder kurz darauf. <br><br>Deshalb wünschen wir uns auch dieses Jahr zum Geburtstag keine Geschenke, sondern wir wollen gemeinsam mit Euch hunderten Kindern in einem der ärmsten Ländern der Welt auch eine  sichere Geburt ermöglichen!<br><br>Wie genau, wo genau und was genau erfahrt ihr im Video :) Eins vorab: Es ist ein wahnsinnig tolles und inspirierendes Projekt, das wir mit ganzem Herzen unterstützen. Und dann: Spendet was das Zeug hält und teilt das Video direkt auf Facebook oder per Email und ladet Eure Freunde, Familie, Verwandte, Bekannte ein, dass sie auch mitmachen. Gemeinsam packen wir das!<br><br>Hier ein paar Beispiele, was Eure Spende bewirken kann:<br>- Mit nur 25€ können 100 Urintests an schwangeren Frauen durchgeführt werden, um herauszufinden ob es dem Kind gut geht<br>- Mit nur 40€ kann eine Hebamme für eine ganze Woche ausgebildet und bezahlt werden<br>- Mit nur 67€ kann das Hebammenmobil mit 3 Mitarbeitern (Arzt, Hebamme, Fahrer) für einen ganzen Abend finanziert werden. Unfassbar, oder?<br>- Mit 200€ kann ein Hämoglobinmessgerät für die Schwangerschaftsvorsorge angeschafft werden und hunderten Frauen eine sicherere Geburt ermöglichen<br>- Mit 220€ kann ein neuer Truck-Reifen für das Hebammenmobil gekauft werden<br>- Mit ganzen 3000€ kann ein dringend benötigtes mobiles Ultraschallgerät für die Untersuchung des Babies im Bauch besorgt werden<br><br>*Die Geschichte von Lanto wie sie im Spendenrap erzählt wird, ist wahr. Die Bilder im Video sind zum großen Teil direkt aus Madagaskar und vom Hebammenmobil, einige sind auch aus anderen afrikanischen Ländern, um das Erzählen dieser magischen Geschichte zu ermöglichen.<br><br>------<br>A wonder occurred on 24th of February: Our daughter Liv was born.<br><br>Thanks to the amazing treatment by the doctors and midwives, Liv came into the world healthy. Unfortunately, the reality in many countries looks different: Children die at birth or shortly after.<br><br>That's why we do not ask for presents again this year, but want to help hundreds of children in one of the poorest countries on Earth have such a safe birth. <br><br>How and where and what exactly, you can find out in the video. One thing: It's an amazing and inspiring project, that we support from the bottom of our hearts. And then: Donate :) And afterwards, share this video on Facebook, send it by email, tell your family about it! Together we can make it!<br><br>No matter if 20, 50, 100, 200 Euros, Dollars, Pounds – every donation matters.",
      "tax_deductible": true,
      "donations_prohibited": false,
      "closed_at": null,
      "donor_count": 349,
      "donated_amount_in_cents": 1689048,
      "requested_amount_in_cents": 1770000,
      "progress_percentage": 95,
      "contact": {
        "id": 176951,
        "name": "Christoph, Jona und Liv ..",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/176/951/fill_100x100_beide.jpg"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/176/951/crop_original_beide.jpg"
            }
          ]
        },
        "links": [
          {
            "rel": "platform",
            "href": "https://www.betterplace.org/de/users/christoph_s34"
          },
          {
            "rel": "contact_data",
            "href": "https://api.betterplace.org/de/api_v4/users/176951/contact_data.json"
          }
        ]
      },
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/fill_960x500_Screen_Shot_2016-04-12_at_01.52.20.png"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/fill_730x380_Screen_Shot_2016-04-12_at_01.52.20.png"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/fill_618x322_Screen_Shot_2016-04-12_at_01.52.20.png"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/fill_410x214_Screen_Shot_2016-04-12_at_01.52.20.png"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/fill_270x141_Screen_Shot_2016-04-12_at_01.52.20.png"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/027/767/crop_original_Screen_Shot_2016-04-12_at_01.52.20.png"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/27767.json"
        },
        {
          "rel": "featured_projects",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/27767/featured_projects.json"
        },
        {
          "rel": "forwardings",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/27767/forwardings.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/fundraising-events/27767-christoph-jona-liv-geburtstags-spendenrap-2016"
        },
        {
          "rel": "new_client_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/27767/client_donations/new?client_id=%7Bclient_id%7D",
          "templated": true
        },
        {
          "rel": "new_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/27767/donations/new"
        }
      ]
    },
    {
      "id": 28024,
      "created_at": "2016-04-26T18:21:17+02:00",
      "updated_at": "2016-06-05T16:45:23+02:00",
      "content_updated_at": "2016-05-19T11:27:16+02:00",
      "title": "Viva con Agua & Clueso: Love the people!",
      "description": "Nach neun Jahren Unterstützung macht sich Musiker und All-Time-Supporter Clueso Ende Mai gemeinsam mit Viva con Agua-Mitbegründer Michael Fritz auf den Weg nach Äthiopien!<br><br>Ob beim gemeinsamen Besuch der unterstützten Wasserprojekte der Welthungerhilfe oder in Musik-Sessions mit äthiopischen Musikern - ganz im Viva con Agua-Style werden sich internationale Aktivisten und Künstler für die gemeinsame Vision aktiv: ALLE FÜR WASSER - WASSER FÜR ALLE<br><br>Mit Äthiopien hat Viva con Agua eine ganz besondere Verbindung! Schließlich war es im Jahre 2006 das erste VCA-Projektland. Seitdem findet ein reger Austausch mit gegenseitigen Besuchen statt. Nicht zuletzt daher liegt uns das Land besonders am Herzen. Es ist uns wichtig, schnellstmöglich einen weiteren positiven Beitrag dort zu leisten, um die erheblichen Herausforderungen im Bereich der Wasserversorgung zu meistern.<br><br>Die Projektbesuche mit Clueso werden in Bahir Dar und Sodo stattfinden. 2 Orte, in denen Viva con Agua schon seit vielen Jahren zusammen mit der Welthungerhilfe und äthiopischen Partnerorganisationen Zugang zu sauberem Trinkwasser ermöglicht.  <br><br>DEINE SPENDE:<br>Wenn du die Wasserprojekte in Äthiopien unterstützen möchtest, kannst du hier ganz einfach online an Viva con Agua spenden! Als Orientierung hier zwei kurze Beispiele, was deine Spende ermöglichen kann:<br><br>25€<br>Zugang zu sauberem Trinkwasser für 6 Menschen in Sodo. Insgesamt erreichen wir mit dem  Wasserprojekt ca. 17.700 Menschen in der Region rund um Sodo, welche im Süden Äthiopiens liegt.  <br><br>50€<br>Zugang zu sauberem Trinkwasser für 15 Menschen in Bahir Dar. Insgesamt erreichen wir mit dem Wasserprojekt ca. 137.000 Menschen in der drittgrößten Stadt Äthiopiens.",
      "tax_deductible": true,
      "donations_prohibited": false,
      "closed_at": null,
      "donor_count": 39,
      "donated_amount_in_cents": 83200,
      "requested_amount_in_cents": null,
      "progress_percentage": null,
      "contact": {
        "id": 328374,
        "name": "Moritz M.",
        "picture": {
          "fallback": true,
          "links": [
            {
              "rel": "fill_100x100",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/328/374/fill_100x100_VCA_Betterplace_Profilbild.jpg"
            },
            {
              "rel": "original",
              "href": "https://asset1.betterplace.org/uploads/user/profile_picture/000/328/374/crop_original_VCA_Betterplace_Profilbild.jpg"
            }
          ]
        },
        "links": [
          {
            "rel": "platform",
            "href": "https://www.betterplace.org/de/users/moritz_m10"
          },
          {
            "rel": "contact_data",
            "href": "https://api.betterplace.org/de/api_v4/users/328374/contact_data.json"
          }
        ]
      },
      "profile_picture": {
        "fallback": true,
        "links": [
          {
            "rel": "fill_960x500",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/fill_960x500_Clueso_betterplace2.jpg"
          },
          {
            "rel": "fill_730x380",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/fill_730x380_Clueso_betterplace2.jpg"
          },
          {
            "rel": "fill_618x322",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/fill_618x322_Clueso_betterplace2.jpg"
          },
          {
            "rel": "fill_410x214",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/fill_410x214_Clueso_betterplace2.jpg"
          },
          {
            "rel": "fill_270x141",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/fill_270x141_Clueso_betterplace2.jpg"
          },
          {
            "rel": "original",
            "href": "https://asset1.betterplace.org/uploads/group/profile_picture/000/028/024/crop_original_Clueso_betterplace2.jpg"
          }
        ]
      },
      "links": [
        {
          "rel": "self",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/28024.json"
        },
        {
          "rel": "featured_projects",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/28024/featured_projects.json"
        },
        {
          "rel": "forwardings",
          "href": "https://api.betterplace.org/de/api_v4/fundraising_events/28024/forwardings.json"
        },
        {
          "rel": "platform",
          "href": "https://www.betterplace.org/de/fundraising-events/28024-viva-con-agua-clueso-love-the-people"
        },
        {
          "rel": "new_client_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/28024/client_donations/new?client_id=%7Bclient_id%7D",
          "templated": true
        },
        {
          "rel": "new_donation",
          "href": "https://www.betterplace.org/de/fundraising-events/28024/donations/new"
        }
      ]
    }
  ]
}
```


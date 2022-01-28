# WorldMap for Blazor
This component shows a map for using it with [Blazor WebAssembly](https://www.puresourcecode.com/tag/blazor-webassembly/) and [Blazor Server](https://www.puresourcecode.com/tag/blazor-server/). The components is build with .NET6.
The map is build with [jqvmap](https://github.com/10bestdesign/jqvmap). `jquery` is required.

Now, usually in connection with the map, we want to display flags or icons. For that, you can use other my component that allows you to use [SVG image for icons and flags](https://www.puresourcecode.com/dotnet/blazor/svg-icons-and-flags-for-blazor/).

You can see the component is action on this [website](https://worldmap.puresourcecode.com/). The full source code is on [GitHub](https://github.com/erossini/BlazorWorldMap). For any comment or question, please use my [forum](https://www.puresourcecode.com/forum/) in the [WorldMap section](https://www.puresourcecode.com/forum/worldmap-for-blazor/).

## Installation
Fist, you have to add the component from NuGet. Then, open your `index.html` or `_Host` and add at the end of the page the following scripts:

```
<script src="/_content/PSC.Blazor.Components.WorldMap/js/worldmap.js"></script>
```

The first script is the jqvmap library version 1.5.0 because I'm using this version to create the components. You can use other sources for it but maybe you can face issues in other versions.

Then, open your `_Imports.razor` and add the following:

```
@using PSC.Blazor.Components.WorldMap
@using PSC.Blazor.Components.WorldMap.Enums
```

I recommend to add also the library [PSC.Extensions](https://www.nuget.org/packages/PSC.Extensions) to convert an `enum` in a string. See the example below.

```
@using PSC.Extensions
```

## Add a new map
In your page you can create a new chart adding this code

```
<WorldMap Values="@values" TextTooltip=": {0} visitors" RegionSelect="@OnRegionSelect" 
    SelectedRegions="@SelectedRegions" SelectChanged="@SelectedChanged"
    PinMode="PinMode.Id" Pins="@pins" />

@code {
    string SelectedRegions = "it, ru";
    List<string> Selection = new List<string>();
    Dictionary<string, string> pins = new Dictionary<string, string>()
    {
        { "it", "svgIcon" }
    };

    Dictionary<string, string> values = new Dictionary<string, string>()
        {
            { World.UnitedKingdom.GetDescription(), "15" },
            { World.Italy.GetDescription(), "7.5" },
            { World.Australia.GetDescription(), "9" },
        };

    Task OnRegionSelect(ChangeData data)
    {
        Console.WriteLine($"Selected {data.Code} / {data.Region}");
        return Task.CompletedTask;
    }

    Task SelectedChanged(List<string> slc)
    {
        Selection = slc;
        return Task.CompletedTask;
    }
}
```

So, with this code you create the map in the followinf screenshot

![World Map Screenshot](https://user-images.githubusercontent.com/9497415/150774328-82a1e5a2-5f1a-46f4-924f-d8c28058ec92.png)

## Add the map to your project

### Countries

| Country   | File name |
|-----------|-----------|
| **World** | jquery.vmap.world.js |
| Algeria   | jquery.vmap.algeria.js |
| Argentina | jquery.vmap.argentina.js |
| Brazil    | jquery.vmap.brazil.js |
| Canada    | jquery.vmap.canada.js |
| Croatia   | jquery.vmap.croatia.js |
| France    | jquery.vmap.france.js |
| Germany   | jquery.vmap.germany.js |
| Greece    | jquery.vmap.greece.js |
| Indonesia | jquery.vmap.indonesia.js |
| Iran      | jquery.vmap.iran.js |
| Iraq      | jquery.vmap.iraq.js |
| Poland    | jquery.vmap.poland.js |
| Russia    | jquery.vmap.russia.js |
| Serbia    | jquery.vmap.serbia.js |
| Tunisia   | jquery.vmap.tunisia.js |
| Turkey    | jquery.vmap.turkey.js |
| Ukraine   | jquery.vmap.ukraine.js |
| Usa       | jquery.vmap.usa.js |
| Venezuela | jquery.vmap.venezuela.js |

### Regions
| Region        | File name |
|---------------|-----------|
| Europe        | jquery.vmap.europe.js |
| France        | jquery.vmap.new_regions_france.js |
| USA countries | jquery.vmap.usa.counties.js |
| USA Districts | jquery.vmap.usa.districts.js |

### Continents
| Continent     | File name |
|---------------|-----------|
| Africa        | jquery.vmap.africa.js |
| Asia          | jquery.vmap.asia.js |
| Australia     | jquery.vmap.australia.js |
| Europe        | jquery.vmap.europe.js |
| North America | jquery.vmap.north-america.js |
| South America | jquery.vmap.south-america.js |

## Configuration settings
| Property | Description | Default |
|----------|-------------|---------|
| Map      |  Map you want to load. Must include the javascript file with the name of the map you want. Available maps with this library are **world_en**, **usa_en**, **europe_en** and **germany_en** | world_en |
| BackgroundColor | Background color of map container in any CSS compatible format. | #a5bfdd |
| BorderColor | Border Color to use to outline map objects | #818181 |
| BorderOpacity | Border Opacity to use to outline map objects (use anything from 0-1, e.g. 0.5) | 0.25 |
| BorderWidth | Border Width to use to outline map objects | 1 |
| Color | Color of map regions. | #f4f3f0 |
| Colors | Colors of individual map regions. Keys of the colors objects are country codes according to ISO 3166-1 alpha-2 standard. Keys of colors must be in lower case. | |
| EnableZoom | Whether to Enable Map Zoom (true or false) | true |
| Height | Height of the map container | 300px |
| HoverColor | Color of the region when mouse pointer is over it. | #c9dfaf |
| HoverColors | Colors of individual map regions when mouse pointer is over it. Keys of the colors objects are country codes according to ISO 3166-1 alpha-2 standard. Keys of colors must be in lower case. | |
| HoverOpacity | Opacity of the region when mouse pointer is over it. | |
| NormalizeFunction | This function can be used to improve results of visualizations for data with non-linear nature. Function gets raw value as the first parameter and should return value which will be used in calculations of color, with which particular region will be painted. | linear |
| ScaleColors | This option defines colors, with which regions will be painted when you set option values. Array scaleColors can have more then two elements. Elements should be strings representing colors in RGB hex format. | ['#b6d6ff', '#005ace'] |
| SelectedColor | Color for a region when you select it | #333333 |
| SelectedRegions | This is the Region that you are looking to have preselected (two letter ISO code, defaults to null). See Region section | null | 
| MultiSelectRegion | Whether to enable more than one region to be selected at a time. |  |
| ShowLabels | Whether to show ISO Code Labels (true or false) | true |
| ShowTooltip | Whether to show Tooltips on Mouseover (true or false) | true |
| Width | Width of the map container | 100% |
| Values | Dictionary of the value to use for each country | null |

## Events
| Event | Description |
|-------|-------------|
| onLoad | Callback function which will be called when map is loading, returning the map event and map details. |
| onLabelShow | Callback function which will be called before label is shown. Label DOM object and country code will be passed to the callback as arguments. |
| onRegionOver | Callback function which will be called when the mouse cursor enters the region path. Country code will be passed to the callback as argument. |
| onRegionOut | Callback function which will be called when the mouse cursor leaves the region path. Country code will be passed to the callback as argument. |
| onRegionClick | Callback function which will be called when the user clicks the region path. Country code will be passed to the callback as argument. This callback may be called while the user is moving the map. If you need to distinguish between a "real" click and a click resulting from moving the map |
| onRegionSelect | Callback function which will be called when the selects a region. Country code will be passed to the callback as argument. |
| onRegionDeselect | Callback function which will be called when the deselects a region. Country code will be passed to the callback as argument. |
| onResize | Callback function which will be called when the map is resized.  Return event, width & height. |

# Regions and enums
## World
| Country code | Region name |
|-------------|-------------|
| AE  |  United Arab Emirates |
| AF  |  Afghanistan |
| AG  |  Antigua and Barbuda |
| AL  |  Albania |
| AM  |  Armenia |
| AO  |  Angola |
| AR  |  Argentina |
| AT  |  Austria |
| AU  |  Australia |
| AZ  |  Azerbaijan |
| BA  |  Bosnia and Herzegovina |
| BB  |  Barbados |
| BD  |  Bangladesh |
| BE  |  Belgium |
| BF  |  Burkina Faso |
| BG  |  Bulgaria |
| BI  |  Burundi |
| BJ  |  Benin |
| BN  |  Brunei Darussalam |
| BO  |  Bolivia |
| BR  |  Brazil |
| BS  |  Bahamas |
| BT  |  Bhutan |
| BW  |  Botswana |
| BY  |  Belarus |
| BZ  |  Belize |
| CA  |  Canada |
| CD  |  Congo |
| CF  |  Central African Republic |
| CG  |  Congo |
| CH  |  Switzerland |
| CI  |  Cote d'Ivoire |
| CL  |  Chile |
| CM  |  Cameroon |
| CN  |  China |
| CO  |  Colombia |
| CR  |  Costa Rica |
| CU  |  Cuba |
| CV  |  Cape Verde |
| CY  |  Cyprus |
| CZ  |  Czech Republic |
| DE  |  Germany |
| DJ  |  Djibouti |
| DK  |  Denmark |
| DM  |  Dominica |
| DO  |  Dominican Republic |
| DZ  |  Algeria |
| EC  |  Ecuador |
| EE  |  Estonia |
| EG  |  Egypt |
| ER  |  Eritrea |
| ES  |  Spain |
| ET  |  Ethiopia |
| FI  |  Finland |
| FJ  |  Fiji |
| FK  |  Falkland Islands |
| FR  |  France |
| GA  |  Gabon |
| GB  |  United Kingdom |
| GD  |  Grenada |
| GE  |  Georgia |
| GF  |  French Guiana |
| GH  |  Ghana |
| GL  |  Greenland |
| GM  |  Gambia |
| GN  |  Guinea |
| GQ  |  Equatorial Guinea |
| GR  |  Greece |
| GT  |  Guatemala |
| GW  |  Guinea-Bissau |
| GY  |  Guyana |
| HN  |  Honduras |
| HR  |  Croatia |
| HT  |  Haiti |
| HU  |  Hungary |
| ID  |  Indonesia |
| IE  |  Ireland |
| IL  |  Israel |
| IN  |  India |
| IQ  |  Iraq |
| IR  |  Iran |
| IS  |  Iceland |
| IT  |  Italy |
| JM  |  Jamaica |
| JO  |  Jordan |
| JP  |  Japan |
| KE  |  Kenya |
| KG  |  Kyrgyz Republic |
| KH  |  Cambodia |
| KM  |  Comoros |
| KN  |  Saint Kitts and Nevis |
| KP  |  North Korea |
| KR  |  South Korea |
| KW  |  Kuwait |
| KZ  |  Kazakhstan |
| LA  |  Lao People's Democratic Republic |
| LB  |  Lebanon |
| LC  |  Saint Lucia |
| LK  |  Sri Lanka |
| LR  |  Liberia |
| LS  |  Lesotho |
| LT  |  Lithuania |
| LV  |  Latvia |
| LY  |  Libya |
| MA  |  Morocco |
| MD  |  Moldova |
| MG  |  Madagascar |
| MK  |  Macedonia |
| ML  |  Mali |
| MM  |  Myanmar |
| MN  |  Mongolia |
| MR  |  Mauritania |
| MT  |  Malta |
| MU  |  Mauritius |
| MV  |  Maldives |
| MW  |  Malawi |
| MX  |  Mexico |
| MY  |  Malaysia |
| MZ  |  Mozambique |
| NA  |  Namibia |
| NC  |  New Caledonia |
| NE  |  Niger |
| NG  |  Nigeria |
| NI  |  Nicaragua |
| NL  |  Netherlands |
| NO  |  Norway |
| NP  |  Nepal |
| NZ  |  New Zealand |
| OM  |  Oman |
| PA  |  Panama |
| PE  |  Peru |
| PF  |  French Polynesia |
| PG  |  Papua New Guinea |
| PH  |  Philippines |
| PK  |  Pakistan |
| PL  |  Poland |
| PT  |  Portugal |
| PY  |  Paraguay |
| QA  |  Qatar |
| RE  |  Reunion |
| RO  |  Romania |
| RS  |  Serbia |
| RU  |  Russian Federationß |
| RW  |  Rwanda |
| SA  |  Saudi Arabia |
| SB  |  Solomon Islands |
| SC  |  Seychelles |
| SD  |  Sudan |
| SE  |  Sweden |
| SI  |  Slovenia |
| SK  |  Slovakia |
| SL  |  Sierra Leone |
| SN  |  Senegal |
| SO  |  Somalia |
| SR  |  Suriname |
| ST  |  Sao Tome and Principe |
| SV  |  El Salvador |
| SY  |  Syrian Arab Republic |
| SZ  |  Swaziland |
| TD  |  Chad |
| TG  |  Togo |
| TH  |  Thailand |
| TJ  |  Tajikistan |
| TL  |  Timor-Leste |
| TM  |  Turkmenistan |
| TN  |  Tunisia |
| TR  |  Turkey |
| TT  |  Trinidad and Tobago |
| TW  |  Taiwan |
| TZ  |  Tanzania |
| UA  |  Ukraine |
| UG  |  Uganda |
| US  |  United States of America |
| UY  |  Uruguay |
| UZ  |  Uzbekistan |
| VE  |  Venezuela |
| VN  |  Vietnam |
| VU  |  Vanuatu |
| YE  |  Yemen |
| ZA  |  South Africa |
| ZM  |  Zambia |
| ZW  |  Zimbabwe |

## USA
| District code | Region name |
|-------------|-------------|
| AK  |  Alaska |
| AL  |  Alabama |
| AR  |  Arkansas |
| AZ  |  Arizona |
| CA  |  California |
| CO  |  Colorado |
| CT  |  Connecticut |
| DC  |  District of Columbia |
| DE  |  Delaware |
| FL  |  Florida |
| GA  |  Georgia |
| HI  |  Hawaii |
| IA  |  Iowa |
| ID  |  Idaho |
| IL  |  Illinois |
| IN  |  Indiana |
| KS  |  Kansas |
| KY  |  Kentucky |
| LA  |  Louisiana |
| MA  |  Massachusetts |
| MD  |  Maryland |
| ME  |  Maine |
| MI  |  Michigan |
| MN  |  Minnesota |
| MO  |  Missouri |
| MS  |  Mississippi |
| MT  |  Montana |
| NC  |  North Carolina |
| ND  |  North Dakota |
| NE  |  Nebraska |
| NH  |  New Hampshire |
| NJ  |  New Jersey |
| NM  |  New Mexico |
| NV  |  Nevada |
| NY  |  New York |
| OH  |  Ohio |
| OK  |  Oklahoma |
| OR  |  Oregon |
| PA  |  Pennsylvania |
| RI  |  Rhode Island |
| SC  |  South Carolina |
| SD  |  South Dakota |
| TN  |  Tennessee |
| TX  |  Texas |
| UT  |  Utah |
| VA  |  Virginia |
| VT  |  Vermont |
| WA  |  Washington |
| WI  |  Wisconsin |
| WV  |  West Virginia |
| WY  |  Wyoming |

## Europe
| Country code | Region name |
|-------------|-------------|
| AD  |  Andorra |
| AL  |  Albania |
| AM  |  Armenia |
| AT  |  Austria |
| AZ  |  Azerbaijan |
| BA  |  Bosnia and Herzegovina |
| BE  |  Belgium |
| BG  |  Bulgaria |
| BY  |  Belarus |
| CH  |  Switzerland |
| CY  |  Cyprus |
| CZ  |  Czech Republic |
| DE  |  Germany |
| DK  |  Denmark |
| DZ  |  Algeria |
| EE  |  Estonia |
| ES  |  Spain |
| FI  |  Finland |
| FR  |  France |
| GB  |  United Kingdom |
| GE  |  Georgia |
| GL  |  Greenland |
| GR  |  Greece |
| HR  |  Croatia |
| HU  |  Hungary |
| IE  |  Ireland |
| IL  |  Israel |
| IQ  |  Iraq |
| IR  |  Iran |
| IS  |  Iceland |
| IT  |  Italy |
| JO  |  Jordan |
| KZ  |  Kazakhstan |
| LB  |  Lebanon |
| LI  |  Liechtenstein |
| LT  |  Lithuania |
| LU  |  Luxembourg |
| LV  |  Latvia |
| MA  |  Morocco |
| MC  |  Monaco |
| MD  |  Moldova |
| ME  |  Montenegro |
| MK  |  Macedonia |
| MT  |  Malta |
| NL  |  Netherlands |
| NO  |  Norway |
| PL  |  Poland |
| PT  |  Portugal |
| RO  |  Romania |
| RU  |  Russian Federation |
| SA  |  Saudi Arabia |
| SE  |  Sweden |
| SI  |  Slovenia |
| SK  |  Slovakia |
| SM  |  San Marino |
| SR  |  Suriname |
| SY  |  Syrian Arab Republic |
| TM  |  Turkmenistan |
| TN  |  Tunisia |
| TR  |  Turkey |
| UA  |  Ukraine |

## Germany
| Region code | Region name |
|-------------|-------------|
| BB  |  Brandenburg |
| BE  |  Berlin |
| BW  |  Baden-W&Atilde;rttemberg |
| BY  |  Bayern |
| HB  |  Bremen |
| HE  |  Hessen |
| HH  |  Hamburg |
| MV  |  Mecklenburg-Vorpommern |
| NI  |  Niedersachsen |
| NW  |  Nordrhein-Westfalen |
| RP  |  Rheinland-Pfalz |
| SH  |  Schleswig-Holstein |
| SL  |  Saarland |
| SN  |  Sachsen |
| ST  |  Sachsen-Anhalt |
| TH  |  Th&Atilde;ri |

## Russia
| Region code | Region name |
|-------------|-------------|
| CH  |  Chukotka Autonomous Okrug |
| KA  |  Kamchatka Krai |
| MA  |  Magadan Oblast |
| SA  |  Sakha Republic |
| AM  |  Amur Oblast |
| PR  |  Primorsky Krai |
| EU  |  Jewish Autonomous Oblast |
| HA  |  Khabarovsk Krai |
| SH  |  Sakhalin Oblast |
| OM  |  Omsk Oblast |
| NV  |  Novosibirsk Oblast |
| AL  |  Altai Krai |
| LT  |  Altai Republic |
| TV  |  Tuva Republic |
| HK  |  Republic of Khakassia |
| KM  |  Kemerovo Oblast |
| TM  |  Tomsk Oblast |
| ZB  |  Zabaykalsky Krai |
| BR  |  Buryat Republic |
| IR  |  Irkutsk Oblast |
| KR  |  Krasnoyarsk Krai |
| YA  |  Yamalo-Nenets Autonomous Okrug |
| HT  |  Khanty-Mansi Autonomous Okrug |
| TU  |  Tyumen Oblast |
| KU  |  Kurgan Oblast |
| CL  |  Chelyabinsk Oblast |
| SV  |  Sverdlovsk Oblast |
| AR  |  Arkhangelsk Oblast |
| NE  |  Nenets Autonomous Okrug |
| KO  |  Komi Republic |
| MU  |  Murmansk Oblast |
| VO  |  Vologda Oblast |
| NO  |  Novgorod Oblast |
| PS  |  Pskov Oblast |
| LE  |  Leningrad Oblast |
| KL  |  Republic of Karelia |
| KN  |  Kaliningrad Oblast |
| DA  |  Republic of Dagestan |
| ST  |  Stavropol Krai |
| SO  |  Republic of North Ossetia-Alania |
| KB  |  Kabardino-Balkar Republic |
| KH  |  Karachay-Cherkess Republic |
| CC  |  Chechen Republic |
| IN  |  Republic of Ingushetia |
| AD  |  Republic of Adygea |
| KS  |  Krasnodar Krai |
| RO  |  Rostov Oblast |
| KK  |  Republic of Kalmykia |
| AS  |  Astrakhan Oblast |
| VL  |  Volgograd Oblast |
| TR  |  Tver Oblast |
| SM  |  Smolensk Oblast |
| BN  |  Bryansk Oblast |
| KY  |  Kursk Oblast |
| BL  |  Belgorod Oblast |
| OR  |  Oryol Oblast |
| KJ  |  Kaluga Oblast |
| TL  |  Tula Oblast |
| LP  |  Lipetsk Oblast |
| MC  |  Moscow Oblast |
| RZ  |  Ryazan Oblast |
| TB  |  Tambov Oblast |
| VM  |  Vladimir Oblast |
| IV  |  Ivanovo Oblast |
| YR  |  Yaroslavl Oblast |
| KT  |  Kostroma Oblast |
| NN  |  Nizhny Novgorod Oblast |
| MR  |  Republic of Mordovia |
| PZ  |  Penza Oblast |
| SR  |  Saratov Oblast |
| SS  |  Samara Oblast |
| OB  |  Orenburg Oblast |
| BS  |  Republic of Bashkortostan |
| UL  |  Ulyanovsk Oblast |
| CU  |  Chuvash Republic |
| TA  |  Republic of Tatarstan |
| ML  |  Mari El Republic |
| UD  |  Udmurt Republic |
| KI  |  Kirov Oblast |
| PE  |  Perm Krai |
| VN  |  Voronezh Oblast |

---

## Other Blazor components

| Component name | Forum | Description |
|---|---|---|
| Chart.js for Blazor | [Forum](https://www.puresourcecode.com/forum/forum/chart-js-for-blazor/) | Component for Blazor WebAssembly and Blazor Server for creating graphs using Chart.js |
| [DataTable for Blazor](https://www.puresourcecode.com/dotnet/net-core/datatable-component-for-blazor/) | [Forum](https://www.puresourcecode.com/forum/forum/datatables/) | DataTable component for Blazor WebAssembly and Blazor Server |
| [Markdown editor for Blazor](https://www.puresourcecode.com/dotnet/blazor/markdown-editor-with-blazor/) | [Forum](https://www.puresourcecode.com/forum/forum/markdown-editor-for-blazor/) |  This is a Markdown Editor for use in Blazor. It contains a live preview as well as an embeded help guide for users. |
| [Modal dialog for Blazor](https://www.puresourcecode.com/dotnet/blazor/modal-dialog-component-for-blazor/) | [Forum](https://www.puresourcecode.com/forum/forum/modal-dialog-for-blazor/) |  Simple Modal Dialog for Blazor WebAssembly |
| [PSC.Extensions](https://www.puresourcecode.com/dotnet/net-core/a-lot-of-functions-for-net5/) | [Forum](https://www.puresourcecode.com/forum/forum/psc-extensions/) |  A lot of functions for .NET5 in a NuGet package that you can download for free. We collected in this package functions for everyday work to help you with claim, strings, enums, date and time, expressions... |
| [Quill for Blazor](https://www.puresourcecode.com/dotnet/blazor/create-a-blazor-component-for-quill/) | [Forum](https://www.puresourcecode.com/forum/forum/quill-for-blazor/) |  Quill Component is a custom reusable control that allows us to easily consume Quill and place multiple instances of it on a single page in our Blazor application |
| [Segment for Blazor](https://www.puresourcecode.com/dotnet/blazor/segment-control-for-blazor/) | [Forum](https://www.puresourcecode.com/forum/forum/segments-for-blazor/) |  This is a Segment component for Blazor Web Assembly and Blazor Server |
| [Tabs for Blazor](https://www.puresourcecode.com/dotnet/blazor/tabs-control-for-blazor/) | [Forum](https://www.puresourcecode.com/forum/forum/tabs-for-blazor/) |  This is a Tabs component for Blazor Web Assembly and Blazor Server |

## More examples and documentation
*   [Write a reusable Blazor component](https://www.puresourcecode.com/dotnet/blazor/write-a-reusable-blazor-component/)
*   [Getting Started With C# And Blazor](https://www.puresourcecode.com/dotnet/net-core/getting-started-with-c-and-blazor/)
*   [Setting Up A Blazor WebAssembly Application](https://www.puresourcecode.com/dotnet/blazor/setting-up-a-blazor-webassembly-application/)
*   [Working With Blazor Component Model](https://www.puresourcecode.com/dotnet/blazor/working-with-blazors-component-model/)
*   [Secure Blazor WebAssembly With IdentityServer4](https://www.puresourcecode.com/dotnet/blazor/secure-blazor-webassembly-with-identityserver4/)
*   [Blazor Using HttpClient With Authentication](https://www.puresourcecode.com/dotnet/blazor/blazor-using-httpclient-with-authentication/)
*   [InputSelect component for enumerations in Blazor](https://www.puresourcecode.com/dotnet/blazor/inputselect-component-for-enumerations-in-blazor/)
*   [Use LocalStorage with Blazor WebAssembly](https://www.puresourcecode.com/dotnet/blazor/use-localstorage-with-blazor-webassembly/)
*   [Modal Dialog component for Blazor](https://www.puresourcecode.com/dotnet/blazor/modal-dialog-component-for-blazor/)
*   [Create Tooltip component for Blazor](https://www.puresourcecode.com/dotnet/blazor/create-tooltip-component-for-blazor/)
*   [Consume ASP.NET Core Razor components from Razor class libraries | Microsoft Docs](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/class-libraries?view=aspnetcore-5.0&tabs=visual-studio)

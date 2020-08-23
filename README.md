# Adding Dynamic Content to the Orchard Core Theme

## Making it East to Manage Your Content

# [YouTube Video](https://youtu.be/nZ45j2zuWYU)

[![OrchardSkillsYouTubeThumbNailDynamic](https://user-images.githubusercontent.com/59172485/90990839-cbae2f00-e561-11ea-823a-bade14948df1.png)](https://youtu.be/nZ45j2zuWYU)

# Introduction

In a previous video, we created an Orchard Core the Creative theme from a Start Bootstrap Template. We just took the index.html and converted it to the layout liquid template. We got everything to work but we really didn't take advantage of the power of the Orchard Core content management system. In this video we will using Orchard Core CMS to integrate dynamic content for the Start Bootstrap theme. So a person, who doesn't know HTML, CSS, or JavaScript can manage their own content. 

![Dynamic-Content-001](https://user-images.githubusercontent.com/59172485/90990813-b0dbba80-e561-11ea-9eb4-845c661b9d1e.png)

Let's refresh what we did on a previous video. This is the theme we created.

![Dynamic-Content-002](https://user-images.githubusercontent.com/59172485/90990814-b20ce780-e561-11ea-9ece-6155722ea9ef.png)

Modify the "ResourceManifest.cs" file to the following code.

```
using OrchardCore.ResourceManagement;

namespace OrchardCore.Themes.TheCreativeTheme
{
    public class ResourceManifest : IResourceManifestProvider
    {
        public void BuildManifests(IResourceManifestBuilder builder)
        {
            var manifest = builder.Add();

            manifest
                .DefineScript("TheCreativeTheme-vendor-jQuery")
                .SetUrl("~/TheCreativeTheme/vendor/jquery/jquery.min.js", "~/TheCreativeTheme/vendor/jquery/jquery.js")
                .SetCdn("https://code.jquery.com/jquery-3.4.1.min.js", "https://code.jquery.com/jquery-3.4.1.js")
                .SetCdnIntegrity("sha384-vk5WoKIaW/vJyUAd9n/wmopsmNhiy+L2Z+SBxGYnUkunIxVxAv/UtMOhba/xskxh", "sha384-mlceH9HlqLp7GMKHrj5Ara1+LvdTZVMx4S1U43/NxCvAkzIo8WJ0FE7duLel3wVo")
                .SetVersion("3.4.1");

            manifest
                .DefineScript("TheCreativeTheme-vendor-jQuery.slim")
                .SetUrl("~/TheCreativeTheme/vendor/jquery/jquery.slim.min.js", "~/TheCreativeTheme/vendor/jquery/jquery.slim.js")
                .SetCdn("https://code.jquery.com/jquery-3.4.1.slim.min.js", "https://code.jquery.com/jquery-3.4.1.slim.js")
                .SetCdnIntegrity("sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n", "sha384-teRaFq/YbXOM/9FZ1qTavgUgTagWUPsk6xapwcjkrkBHoWvKdZZuAeV8hhaykl+G")
                .SetVersion("3.4.1");

            manifest
                .DefineScript("TheCreativeTheme-vendor-jQuery.easing")
                .SetDependencies("TheCreativeTheme-vendor-jQuery")
                .SetUrl("~/TheCreativeTheme/vendor/jquery-easing/jquery.easing.min.js", "~/TheCreativeTheme/vendor/jquery-easing/jquery.easing.js")
                .SetCdn("https://cdn.jsdelivr.net/npm/jquery.easing@1.4.1/jquery.easing.min.js", "https://cdn.jsdelivr.net/npm/jquery.easing@1.4.1/jquery.easing.js")
                .SetCdnIntegrity("sha384-leGYpHE9Tc4N9OwRd98xg6YFpB9shlc/RkilpFi0ljr3QD4tFoFptZvgnnzzwG4Q", "sha384-fwPA0FyfPOiDsglgAC4ZWmBGwpXSZNkq9IG+cM9HL4CkpNQo4xgCDkOIPdWypLMX")
                .SetVersion("1.4.1");

            manifest
                .DefineScript("TheCreativeTheme-vendor-bootstrap")
                .SetDependencies("TheCreativeTheme-vendor-jQuery")
                .SetUrl("~/TheCreativeTheme/vendor/bootstrap/js/bootstrap.min.js", "~/TheCreativeTheme/vendor/bootstrap/js/bootstrap.js")
                .SetCdn("https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js", "https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.js")
                .SetCdnIntegrity("sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM", "sha384-rkSGcquOAzh5YMplX4tcXMuXXwmdF/9eRLkw/gNZG+1zYutPej7fxyVLiOgfoDgi")
                .SetVersion("4.3.1");

            manifest
                .DefineScript("TheCreativeTheme-vendor-bootstrap-bundle")
                .SetDependencies("TheCreativeTheme-vendor-jQuery")
                .SetUrl("~/TheCreativeTheme/vendor/bootstrap/js/bootstrap.bundle.min.js", "~/TheCreativeTheme/vendor/bootstrap/js/bootstrap.bundle.js")
                .SetCdn("https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.bundle.min.js", "https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.bundle.js")
                .SetCdnIntegrity("sha384-xrRywqdh3PHs8keKZN+8zzc5TX0GRTLCcmivcbNJWm2rs5C8PRhcEn3czEjhAO9o", "sha384-szbKYgPl66wivXHlSpJF+CKDAVckMVnlGrP25Sndhe+PwOBcXV9LlFh4MUpRhjIB")
                .SetVersion("4.3.1");

            manifest
                .DefineStyle("TheCreativeTheme-vendor-bootstrap")
                .SetUrl("~/TheCreativeTheme/vendor/bootstrap/css/bootstrap.min.css", "~/TheCreativeTheme/vendor/bootstrap/css/bootstrap.css")
                .SetCdn("https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css", "https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.css")
                .SetCdnIntegrity("sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T", "sha384-t4IGnnWtvYimgcRMiXD2ZD04g28Is9vYsVaHo5LcWWJkoQGmMwGg+QS0mYlhbVv3")
                .SetVersion("4.3.1");

            manifest
                .DefineStyle("TheCreativeTheme-bootstrap-oc")
                .SetUrl("~/TheCreativeTheme/css/bootstrap-oc.min.css", "~/TheCreativeTheme/css/bootstrap-oc.css")
                .SetVersion("1.0.0");
				
            manifest
                .DefineStyle("TheCreativeTheme-vendor-font-awesome")
                .SetUrl("~/TheCreativeTheme/vendor/fontawesome-free/css/all.min.css", "~/TheCreativeTheme/vendor/fontawesome-free/css/all.css")
                .SetCdn("https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.10.2/css/all.min.css", "https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.10.2/css/all.css")
                .SetCdnIntegrity("sha384-rtJEYb85SiYWgfpCr0jn174XgJTn4rptSOQsMroFBPQSGLdOC5IbubP6lJ35qoM9", "sha384-Ex0vLvgbKZTFlqEetkjk2iUgM+H5udpQKFKjBoGFwPaHRGhiWyVI6jLz/3fBm5ht")
                .SetVersion("5.10.2");

            manifest
                .DefineScript("TheCreativeTheme-vendor-font-awesome")
                .SetCdn("https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.10.2/js/all.min.js", "https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.10.2/js/all.js")
                .SetCdnIntegrity("sha384-QMu+Y+eu45Nfr9fmFOlw8EqjiUreChmoQ7k7C1pFNO8hEbGv9yzsszTmz+RzwyCh", "sha384-7/I8Wc+TVwiZpEjE4qTV6M27LYR5Dus6yPGzQZowRtgh+0gDW9BNR9GmII1/YwmG")
                .SetVersion("5.10.2");
        }
    }
}

```



![Dynamic-Content-003](https://user-images.githubusercontent.com/59172485/90990817-b33e1480-e561-11ea-9c58-945b261209d3.png)

Modify the "Startup.cs" file to the following code:

```

using Microsoft.Extensions.DependencyInjection;
using OrchardCore.Modules;
using OrchardCore.ResourceManagement;

namespace OrchardCore.Themes.TheCreativeTheme
{
    public class Startup : StartupBase
    {
        public override void ConfigureServices(IServiceCollection serviceCollection)
        {
            serviceCollection.AddScoped<IResourceManifestProvider, ResourceManifest>();
        }
    }
}

```



![Dynamic-Content-004](https://user-images.githubusercontent.com/59172485/90990818-b3d6ab00-e561-11ea-9fb6-3c84a75ebf20.png)

Modify the "Layout.liquid" file to the following code.

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="author" content="">
  <title>{{ "PageTitle" | shape_new | shape_stringify }}</title>
  {% resources type: "Meta" %}

  <!-- Font Awesome Icons -->
  <link href="/TheCreativeTheme/vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css">

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css?family=Merriweather+Sans:400,700" rel="stylesheet">
  <link href='https://fonts.googleapis.com/css?family=Merriweather:400,300,300italic,400italic,700,700italic' rel='stylesheet' type='text/css'>

  <!-- Plugin CSS -->
  <link href="/TheCreativeTheme/vendor/magnific-popup/magnific-popup.css" rel="stylesheet">

  <!-- Theme CSS - Includes Bootstrap -->
  <link href="/TheCreativeTheme/css/creative.min.css" rel="stylesheet">

  {% resources type: "HeadScript" %}
  {% resources type: "HeadLink" %}
  {% resources type: "Stylesheet" %}
  {% render_section "HeadMeta", required: false %}
</head>

<body id="page-top" dir="{{ Culture.Dir }}">

  <!-- Navigation -->
  <nav class="navbar navbar-expand-lg navbar-light fixed-top py-3" id="mainNav">
    <div class="container">
       <a class="navbar-brand js-scroll-trigger" href="{{ '~/#page-top' | href }}">{{ Site.SiteName }}</a>
       <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">{{ "Menu" | t }}<i class="fas fa-bars ml-1"></i></button>
       {% shape "menu", alias: "alias:main-menu", cache_id: "main-menu", cache_tag: "alias:main-menu" %}
    </div>
  </nav>

  {% render_section "Header", required: false %}
  <div class="nocontainer" id="main">
    {% render_section "Messages", required: false %}
    {% render_section "Content" %}
  </div>
  {% render_section "Footer", required: false %}
  {% resources type: "FootScript" %}

  <!-- Bootstrap core JavaScript -->
  <script src="/TheCreativeTheme/vendor/jquery/jquery.min.js"></script>
  <script src="/TheCreativeTheme/vendor/bootstrap/js/bootstrap.bundle.min.js"></script>

  <!-- Plugin JavaScript -->
  <script src="/TheCreativeTheme/vendor/jquery-easing/jquery.easing.min.js"></script>
  <script src="/TheCreativeTheme/vendor/magnific-popup/jquery.magnific-popup.min.js"></script>

  <!-- Custom scripts for this template -->
  <script src="/TheCreativeTheme/js/creative.min.js"></script>

</body>

</html>

```



![Dynamic-Content-005](https://user-images.githubusercontent.com/59172485/90990819-b507d800-e561-11ea-9d1e-9df7f07eabd4.png)

Modify the "footer.html" file in the "Snippets" folder.

```
<!-- Footer -->
<footer class="bg-light py-5">
    <div class="container">
        <div class="small text-center text-muted">Copyright &copy; 2020 - Start Bootstrap</div>
    </div>
</footer>
```

![Dynamic-Content-007](https://user-images.githubusercontent.com/59172485/90990821-b6390500-e561-11ea-90b7-866e8ce53522.png)

Modify the recipe file "creative.recipe.json" to the following:

```
{
  "name": "The Creative Theme",
  "displayName": "The Creative Theme",
  "description": "Orchard Skills CreativeTheme.",
  "author": "Orchard Skills",
  "website": "https://OrchardSkills.com",
  "version": "1.0.0-rc2",
  "issetuprecipe": true,
  "categories": [ "default" ],
  "tags": [ "Creative" ],

  // The variables are evaluated the first time they are accessed, and reused across steps
  "variables": {
    "landingContentItemId": "[js:uuid()]"
    // "now": "[js: new Date().toISOString()]"
  },

  "steps": [
    {
      "name": "feature",
      "disable": [],
      "enable": [
        // SaaS
        "OrchardCore.HomeRoute",
        "OrchardCore.Admin",
        "OrchardCore.Diagnostics",
        "OrchardCore.DynamicCache",
        "OrchardCore.Features",
        "OrchardCore.Navigation",
        "OrchardCore.Recipes",
        "OrchardCore.Resources",
        "OrchardCore.Roles",
        "OrchardCore.Settings",
        "OrchardCore.Themes",
        "OrchardCore.Users",

        // Content Management
        "OrchardCore.Alias",
        "OrchardCore.Autoroute",
        "OrchardCore.Html",
        "OrchardCore.ContentFields",
        "OrchardCore.ContentPreview",
        "OrchardCore.Contents",
        "OrchardCore.Contents.FileContentDefinition",
        "OrchardCore.ContentTypes",
        "OrchardCore.CustomSettings",
        "OrchardCore.Deployment",
        "OrchardCore.Deployment.Remote",
        "OrchardCore.Feeds",
        "OrchardCore.Flows",
        "OrchardCore.Layers",
        "OrchardCore.Lists",
        "OrchardCore.Liquid",
        "OrchardCore.Markdown",
        "OrchardCore.Media",
        "OrchardCore.Menu",
        "OrchardCore.Queries",
        "OrchardCore.Title",
        "OrchardCore.Templates",
        "OrchardCore.Widgets",

        // Themes
        "TheCreativeTheme",
        "TheAdmin",
        "SafeMode"
      ]
    },
    {
      "name": "themes",
      "admin": "TheAdmin",
      "site": "TheCreativeTheme"
    },
    {
      "name": "settings",
      "HomeRoute": {
        "Action": "Display",
        "Controller": "Item",
        "Area": "OrchardCore.Contents",
        "ContentItemId": "[js: variables('landingContentItemId')]"
      },
      "LayerSettings": {
        "Zones": [ "Footer" ]
      }
    },
    {
      "name": "ContentDefinition",
      "ContentTypes": [
        {
          "Name": "LiquidPage",
          "DisplayName": "Liquid Page",
          "Hidden": false,
          "Settings": {
            "ContentTypeSettings": {
              "Creatable": true,
              "Draftable": true,
              "Versionable": true,
              "Listable": true
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "LiquidPage",
              "Name": "LiquidPage",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "2"
                }
              }
            },
            {
              "PartName": "AutoroutePart",
              "Name": "AutoroutePart",
              "Settings": {
                "AutoroutePartSettings": {
                  "AllowCustomPath": true,
                  "Pattern": "{{ Model.ContentItem | display_text | slugify }}",
                  "ShowHomepageOption": true
                },
                "ContentTypePartSettings": {
                  "Position": "1"
                }
              }
            },
            {
              "PartName": "LiquidPart",
              "Name": "LiquidPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "3"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "HtmlWidget",
          "DisplayName": "Html",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "HtmlWidget",
              "Name": "HtmlWidget",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Page",
          "DisplayName": "Page",
          "Settings": {
            "ContentTypeSettings": {
              "Creatable": true,
              "Draftable": true,
              "Versionable": true,
              "Listable": true,
              "Securable": true
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Page",
              "Name": "Page",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "3"
                }
              }
            },
            {
              "PartName": "AutoroutePart",
              "Name": "AutoroutePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "1"
                },
                "AutoroutePartSettings": {
                  "AllowCustomPath": true,
                  "Pattern": "{{ Model.ContentItem | display_text | slugify }}",
                  "ShowHomepageOption": true
                }
              }
            },
            {
              "PartName": "FlowPart",
              "Name": "FlowPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "2"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "LandingPage",
          "DisplayName": "Landing Page",
          "Settings": {
            "ContentTypeSettings": {
              "Creatable": true,
              "Draftable": true,
              "Versionable": true,
              "Listable": true,
              "Securable": true
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "LandingPage",
              "Name": "LandingPage",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "8"
                }
              }
            },
            {
              "PartName": "AutoroutePart",
              "Name": "AutoroutePart",
              "Settings": {
                "AutoroutePartSettings": {
                  "AllowCustomPath": true,
                  "Pattern": "{{ Model.ContentItem | display_text | slugify }}",
                  "ShowHomepageOption": true
                },
                "ContentTypePartSettings": {
                  "Position": "1"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            },
            {
              "PartName": "BagPart",
              "Name": "Services",
              "Settings": {
                "ContentTypePartSettings": {
                  "DisplayName": "Services",
                  "Description": "Provides a collection behavior for your content item.",
                  "Position": "3"
                },
                "BagPartSettings": {
                  "ContainedContentTypes": [
                    "Service"
                  ]
                }
              }
            },
            {
              "PartName": "BagPart",
              "Name": "Portfolio",
              "Settings": {
                "BagPartSettings": {
                  "ContainedContentTypes": [
                    "Project"
                  ]
                },
                "ContentTypePartSettings": {
                  "DisplayName": "Portfolio",
                  "Description": "Provides a collection behavior for your content item.",
                  "Position": "4"
                }
              }
            }
          ]
        },
        {
          "Name": "Service",
          "DisplayName": "Service",
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Service",
              "Name": "Service",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "2"
                }
              }
            },
            {
              "PartName": "HtmlBodyPart",
              "Name": "HtmlBodyPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "1"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Project",
          "DisplayName": "Project",
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Project",
              "Name": "Project",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "2"
                }
              }
            },
            {
              "PartName": "HtmlBodyPart",
              "Name": "HtmlBodyPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "1"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Container",
          "DisplayName": "Container",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Container",
              "Name": "Container",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            },
            {
              "PartName": "FlowPart",
              "Name": "FlowPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "1"
                }
              }
            }
          ]
        },
        {
          "Name": "Blockquote",
          "DisplayName": "Blockquote",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Blockquote",
              "Name": "Blockquote",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "ImageWidget",
          "DisplayName": "Image",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Image",
              "Name": "Image",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "LiquidWidget",
          "DisplayName": "Liquid",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "LiquidPart",
              "Name": "LiquidPart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Image",
          "DisplayName": "Image",
          "Settings": {
            "ContentTypeSettings": {
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Image",
              "Name": "Image",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            },
            {
              "PartName": "TitlePart",
              "Name": "TitlePart",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Paragraph",
          "DisplayName": "Paragraph",
          "Settings": {
            "ContentTypeSettings": {
              "Draftable": true,
              "Versionable": true,
              "Securable": true,
              "Stereotype": "Widget"
            }
          },
          "ContentTypePartDefinitionRecords": [
            {
              "PartName": "Paragraph",
              "Name": "Paragraph",
              "Settings": {
                "ContentTypePartSettings": {
                  "Position": "0"
                }
              }
            }
          ]
        }
      ],
      "ContentParts": [
        {
          "Name": "HtmlWidget",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "HtmlField",
              "Name": "Content",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Content",
                  "Editor": "Multiline",
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "MenuItem",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "TextField",
              "Name": "Link",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Link",
                  "Position": "0"
                }
              }
            }
          ]
        },
        {
          "Name": "Service",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "TextField",
              "Name": "IconClass",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Icon Class",
                  "Position": "0"
                },
                "TextFieldSettings": {
                  "Hint": "The icon css class from font-awesome. e.g., fa-laptop, fa-shopping-cart, fa-lock"
                }
              }
            }
          ]
        },
        {
          "Name": "Project",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "MediaField",
              "Name": "Image",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Image",
                  "Position": "1"
                },
                "MediaFieldSettings": {
                  "Required": true,
                  "Multiple": false
                }
              }
            },
            {
              "FieldName": "MediaField",
              "Name": "ThumbnailImage",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "ThumbnailImage"
                },
                "MediaFieldSettings": {}
              }
            },
            {
              "FieldName": "TextField",
              "Name": "Category",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Category",
                  "Position": "0"
                },
                "TextFieldSettings": {
                  "Hint": "The category that is displayed below the title"
                }
              }
            }
          ]
        },
        {
          "Name": "Blockquote",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "TextField",
              "Name": "Quote",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Quote",
                  "Position": "0",
                  "Editor": "TextArea"
                }
              }
            }
          ]
        },
        {
          "Name": "Image",
          "Settings": {
            "ContentPartSettings": {
              "Attachable": true
            }
          },
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "MediaField",
              "Name": "Media",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Image",
                  "Position": "0"
                },
                "MediaFieldSettings": {
                  "Required": true,
                  "Multiple": false
                }
              }
            },
            {
              "FieldName": "TextField",
              "Name": "Caption",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Caption",
                  "Position": "1"
                },
                "TextFieldSettings": {
                  "Hint": "A description of the image used as title or alternate text"
                }
              }
            }
          ]
        },
        {
          "Name": "Paragraph",
          "Settings": {},
          "ContentPartFieldDefinitionRecords": [
            {
              "FieldName": "HtmlField",
              "Name": "Content",
              "Settings": {
                "ContentPartFieldSettings": {
                  "DisplayName": "Content",
                  "Position": "0",
                  "Editor": "Wysiwyg"
                }
              }
            }
          ]
        }
      ]
    },
    {
      "name": "content",
      "Data": [
        {
          "ContentItemId": "[js: uuid()]",
          "ContentType": "HtmlWidget",
          "DisplayText": "Footer",
          "Latest": true,
          "Published": true,
          "Owner": "[js: parameters('AdminUsername')]",
          "Author": "[js: parameters('AdminUsername')]",
          "LayerMetadata": {
            "Layer": "Always",
            "Zone": "Footer",
            "RenderTitle": false,
            "Position": 10
          },
          "HtmlWidget": {
            "Content": {
              "Html": "[file:text('Snippets/footer.html')]"
            }
          }
        }
      ]
    },
    {
      "name": "layers",
      "Layers": [
        {
          "Name": "Always",
          "Rule": "true",
          "Description": "The widgets in this layer are displayed on any page of this site."
        },
        {
          "Name": "Homepage",
          "Rule": "isHomepage()",
          "Description": "The widgets in this layer are only displayed on the homepage."
        }
      ]
    },
    {
      "name": "media",
      "Files": [
        {
          "TargetPath": "fullsize/1.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/1.jpg"
        },
        {
          "TargetPath": "fullsize/2.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/2.jpg"
        },
        {
          "TargetPath": "fullsize/3.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/3.jpg"
        },
        {
          "TargetPath": "fullsize/4.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/4.jpg"
        },
        {
          "TargetPath": "fullsize/5.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/5.jpg"
        },
        {
          "TargetPath": "fullsize/6.jpg",
          "SourcePath": "../wwwroot/img/portfolio/fullsize/6.jpg"
        },
        {
          "TargetPath": "thumbnails/1.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/1.jpg"
        },
        {
          "TargetPath": "thumbnails/2.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/2.jpg"
        },
        {
          "TargetPath": "thumbnails/3.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/3.jpg"
        },
        {
          "TargetPath": "thumbnails/4.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/4.jpg"
        },
        {
          "TargetPath": "thumbnails/5.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/5.jpg"
        },
        {
          "TargetPath": "thumbnails/6.jpg",
          "SourcePath": "../wwwroot/img/portfolio/thumbnails/6.jpg"
        }
      ]
    },
    {
      "name": "Content",
      "data": [
        {
          "ContentItemId": "[js:uuid()]",
          "ContentItemVersionId": "[js:uuid()]",
          "ContentType": "Menu",
          "DisplayText": "Main Menu",
          "Latest": true,
          "Published": true,
          "Owner": "[js: parameters('AdminUsername')]",
          "Author": "[js: parameters('AdminUsername')]",
          "MenuPart": {},
          "TitlePart": {
            "Title": "Main Menu"
          },
          "MenuItemsListPart": {
            "MenuItems": [
              {
                "ContentType": "LinkMenuItem",
                "ContentItemId": "[js:uuid()]",
                "LinkMenuItemPart": {
                  "Name": "About",
                  "Url": "~/#about"
                }
              },
              {
                "ContentType": "LinkMenuItem",
                "ContentItemId": "[js:uuid()]",
                "LinkMenuItemPart": {
                  "Name": "Services",
                  "Url": "~/#services"
                }
              },
              {
                "ContentType": "LinkMenuItem",
                "ContentItemId": "[js:uuid()]",
                "LinkMenuItemPart": {
                  "Name": "Portfolio",
                  "Url": "~/#portfolio"
                }
              },
              {
                "ContentType": "LinkMenuItem",
                "ContentItemId": "[js:uuid()]",
                "LinkMenuItemPart": {
                  "Name": "Contact",
                  "Url": "~/#contact"
                }
              }
            ]
          },
          "AliasPart": {
            "Alias": "main-menu"
          }
        },
        {
          "ContentItemId": "[js:uuid()]",
          "ContentItemVersionId": "[js:uuid()]",
          "ContentType": "LandingPage",
          "DisplayText": "[js: parameters('SiteName')]",
          "Latest": true,
          "Published": true,
          "Owner": "[js: parameters('AdminUsername')]",
          "Author": "[js: parameters('AdminUsername')]",
          "LandingPage": {},
          "AutoroutePart": {
            "Path": "home-page",
            "SetHomepage": true
          },
          "TitlePart": {
            "Title": "[js: parameters('SiteName')]"
          },
          "Services": {
            "ContentItems": [
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Service",
                "DisplayText": "Sturdy Themes",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Service": {
                  "IconClass": {
                    "Text": "fa-gem"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Our themes are updated regularly to keep them bug free!"
                },
                "TitlePart": {
                  "Title": "Sturdy Themes"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Service",
                "DisplayText": "Up to Date",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Service": {
                  "IconClass": {
                    "Text": "fa-laptop-code"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "All dependencies are kept current to keep things fresh."
                },
                "TitlePart": {
                  "Title": "Up to Date"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Service",
                "DisplayText": "Ready to Publish",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Service": {
                  "IconClass": {
                    "Text": "fa-globe"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "You can use this design as is, or you can make changes!"
                },
                "TitlePart": {
                  "Title": "Ready to Publish"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Service",
                "DisplayText": "Made with Love",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Service": {
                  "IconClass": {
                    "Text": "fa-heart"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Is it really open source if it's not made with love?"
                },
                "TitlePart": {
                  "Title": "Made with Love"
                }
              }

            ]
          },
          "Portfolio": {
            "ContentItems": [
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Design",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/1.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/1.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Illustrations"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Design items"
                },
                "TitlePart": {
                  "Title": "Design"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Game",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/2.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/2.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Graphic Design"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Game board"
                },
                "TitlePart": {
                  "Title": "Game"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Cameras",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/3.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/3.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Identity"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Vintage cameras"
                },
                "TitlePart": {
                  "Title": "Cameras"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Kitchen",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/4.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/4.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Kitchen"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Kitchen items"
                },
                "TitlePart": {
                  "Title": "Kitchen"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Ruler",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/5.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/5.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Measure"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Folding ruler"
                },
                "TitlePart": {
                  "Title": "Ruler"
                }
              },
              {
                "ContentItemId": "[js:uuid()]",
                "ContentItemVersionId": "[js:uuid()]",
                "ContentType": "Project",
                "DisplayText": "Tools",
                "Latest": false,
                "Published": false,
                "Owner": null,
                "Author": "[js: parameters('AdminUsername')]",
                "Project": {
                  "Image": {
                    "Paths": [
                      "/fullsize/6.jpg"
                    ]
                  },
                  "ThumbnailImage": {
                    "Paths": [
                      "thumbnails/1.jpg"
                    ]
                  },
                  "Category": {
                    "Text": "Tooling"
                  }
                },
                "HtmlBodyPart": {
                  "Html": "Hand tools"
                },
                "TitlePart": {
                  "Title": "Tools"
                }
              }
            ]
          }
        }
      ]
    },
    {
      "name": "Templates",
      "Templates": {
        "Content__LandingPage": {
          "Description": "A template for the Landing Page content type",
          "Content": "[file:text('Snippets/landingpage.liquid')]"
        }
      }
    }

  ]
}

```



![Dynamic-Content-008](https://user-images.githubusercontent.com/59172485/90990823-b6d19b80-e561-11ea-9bb4-ed9e598e0ec6.png)

Run the application by pressing the green play button.



![Dynamic-Content-009](https://user-images.githubusercontent.com/59172485/90990824-b76a3200-e561-11ea-8172-550e870a55d5.png)

Enter in a site name, select the Orchard Skills Creative Recipe, enter in your credentials and then press the "Finish Setup" button.



![Dynamic-Content-010](https://user-images.githubusercontent.com/59172485/90990825-b802c880-e561-11ea-9255-ee4518998312.png)

Congratulations your web application is running.



![Dynamic-Content-011](https://user-images.githubusercontent.com/59172485/90990826-b89b5f00-e561-11ea-8883-547d91de4d00.png)

Go to the Admin Dashboard by appending "/admin" at the end of the URL.



![Dynamic-Content-012](https://user-images.githubusercontent.com/59172485/90990827-b933f580-e561-11ea-97a8-3d26c113b137.png)

Enter your credentials and press the "Log in" button.



![Dynamic-Content-013](https://user-images.githubusercontent.com/59172485/90990828-b933f580-e561-11ea-9f95-10cf79d57b58.png)

Click on "Content" then "Content Items", and finally click on the LandingPage link.



![Dynamic-Content-014](https://user-images.githubusercontent.com/59172485/90990829-b9cc8c00-e561-11ea-9d65-40b3bcd8fa11.png)

Notice you can modify your content inside the Admin Dashboard editors.



![Dynamic-Content-015](https://user-images.githubusercontent.com/59172485/90990830-b9cc8c00-e561-11ea-918b-4015def0d43b.png)

You can even use preview mode and moved content around by using drag and drop.

# Conclusion

Now to summarize. we created an Orchard Core Creative theme from a Start Bootstrap HTML Template. We just took the index.html and converted it to the layout liquid template. We also created a landing page liquid template that had just the necessary HTML to customize the landing page. We took the customization a bit further and added dynamic content for the Menu, Services and Portfolios. We modified the Creative recipe to define and create our menu, services and portfolio custom content. We ran the web application with the custom content enabled. We went to the dashboard and view the dynamic custom services and portfolio. We ran in preview mode, changed the order the services with a mouse, After doing so the content was also changed. With orchard core CMS you can develop a custom theme so that anyone can create, modify or delete their content without knowing HTML, CSS or JavaScript.

# GitHub

The complete source code is located [here](https://github.com/OrchardSkills/OrchardSkills.OrchardCore.DynamicContent).

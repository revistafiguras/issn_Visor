### Agregar issn al visor lens en el archivo lens.js
##### Agregar en esta linea manualmente el issn:  
##### html: a.join(" ") + "ISSN --------"  en la función 38 en la version lens 1.0.0.0

 ``` 38: [function(t, e, n) {
        "use strict";
        var i = t("underscore")`
          , o = t("../node").View
          , r = t("../../../substance/application").$$
          , s = t("../../article_util")
          , a = function(t, e) {
            o.call(this, t, e)
        };
        (a.Prototype = function() {
            this.render = function() {
                o.prototype.render.call(this);
                var t = this.node
                  , e = this.node.document.get("publication_info");
                if (e) {
                    var n, a = e.subjects;
                    if (a)
                        n = e.subject_link ? r(".subjects", {
                            children: i.map(e.getSubjectLinks(), function(t) {
                                return r("a", {
                                    href: t.url,
                                    text: t.name
                                })
                            })
                        }) : r(".subjects", {
                            html: a.join(" ") +  "ISSN 2683-2917" 
                        }),
                        this.content.appendChild(n)
                }
                var c = this.createTextPropertyView(["document", "title"], {
                    classes: "title",
                    elementType: "div"
                });
                this.content.appendChild(c.render().el);
                var l = r(".authors", {
                    children: i.map(t.getAuthors(), function(t) {
                        var e = this.viewFactory.createView(t).render().el;
                        return this.content.appendChild(e),
                        e
                    }, this)
                });
                if (l.appendChild(r(".content-node.text.plain", {
                    children: [r(".content", {
                        text: this.node.document.on_behalf_of
                    })]
                })),
                this.content.appendChild(l),
                e) {
                    var u = e.published_on
                      , p = e.article_type;
                    if (u) {
                        var h = [s.formatDate(u)];
                        if (p)
                            if (e.article_type_link) {
                                var d = e.getArticleTypeLink();
                                h.unshift('<a href="' + d.url + '">' + d.name + "</a>")
                            } else
                                h.unshift(p);
                        this.content.appendChild(r(".published-on", {
                            html: h.join(" ")
                        }))
                    }
                }
                if (e && e.links.length > 0) {
                    var f = r(".links");
                    i.each(e.links, function(t) {
                        if ("json" === t.type && "" === t.url) {
                            var e = JSON.stringify(this.node.document.toJSON(), null, "  ")
                              , n = new Blob([e],{
                                type: "application/json"
                            });
                            f.appendChild(r("a.json", {
                                href: window.URL ? window.URL.createObjectURL(n) : "#",
                                html: '<i class="fa fa-external-link-square"></i> ' + t.name,
                                target: "_blank"
                            }))
                        } else
                            f.appendChild(r("a." + t.type, {
                                href: t.url,
                                html: '<i class="fa fa-external-link-square"></i> ' + t.name,
                                target: "_blank"
                            }))
                    }, this),
                    this.content.appendChild(f)
                }
                if (e) {
                    var g = e.doi;
                    g && this.content.appendChild(r(".doi", {
                        html: 'DOI: <a href="http://dx.doi.org/' + g + '">' + g + "</a>"
                    }))
                }
                return this
            }
        }
        ).prototype = o.prototype,
        a.prototype = new a.Prototype,
        e.exports = a
    }
    , {
        "../../../substance/application": 158,
        "../../article_util": 4,
        "../node": 90,
        underscore: 183
    }] 

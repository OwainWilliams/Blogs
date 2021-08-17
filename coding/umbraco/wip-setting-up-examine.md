# \[WIP\] Setting up Examine

## Getting Setup with ExamineY

* Setup a view with a basic form

```text
 @using (Html.BeginUmbracoForm("Search", "Search", Project.Core.Constants.Site, FormMethod.Get))
                                {
                                    @Html.AntiForgeryToken()

                                    <div class="field_wrap __text">
                                        <div class="label_wrap sronly"><label for="searchbar-input">Search</label></div>
                                        <div class="input_wrap"><input type="text" placeholder="Search..." id="searchbar-input" class="searchBarFocus" value="" name="q" tabindex="-1"></div>
                                    </div>
                                    <div class="submit_wrap">
                                        <button type="submit" tabindex="-1">
                                            <span>Search</span>
                                        </button>
                                    </div>

                                }
```

* Create a Controller with a suitable action method name
* Remember to create a Composer to register your Services!!



{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}




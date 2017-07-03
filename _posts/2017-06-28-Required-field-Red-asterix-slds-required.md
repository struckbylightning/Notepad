---
published: true
---
**Simple code explaining use of slds-required to get red asterixs for input fields label.**

![_slds_required_red_asterix_for_input_controls.png]({{ site.baseurl }}/images/slds_required_red_asterix_for_input_controls.png)

```html
<div class="slds-form-element">
    <label class="slds-form-element__label" for="cusinfocomp-input4">
        <aura:if isTrue="{!v.required}">
            <abbr class="slds-required" title="required" aura:id="emailReq">*											</abbr>
        </aura:if>
        Email Address
    </label>
    <div class="slds-form-element__control">
        <ui:inputText aura:id="cusinfocomp-input4" class="slds-input" value="                                         {!v.contact.Email}" blur="{!c.checkValidate}"/>
    </div>
</div>
```
----
****

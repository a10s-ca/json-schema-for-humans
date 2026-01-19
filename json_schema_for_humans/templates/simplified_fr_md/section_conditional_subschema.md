{% if schema.kw_if %}
Condition particulière:
    {% set first_property =  schema.kw_if | get_first_property %}
    {% if schema.kw_then %}
si ({{ first_property.property_name }} = {{ first_property.const_value | python_to_json }}) alors les propriétés suivantes sont obligatoires

{% set required_props = schema.kw_then.required_properties %}
{% if required_props %}
{% for prop in required_props %}
* {{ prop }}
{% endfor %}
{% endif %}
    {% endif %}
    {% if schema.kw_else %}
Sinon ({{ first_property.property_name }} ≠ {{ first_property.const_value | python_to_json }}) alors les propriétés suivantes sont obligatoires

{% set required_props = schema.kw_else.required_properties %}
{% if required_props %}
{% for prop in required_props %}
* {{ prop }}
{% endfor %}
{% endif %}
    {% endif %}
{% endif %}
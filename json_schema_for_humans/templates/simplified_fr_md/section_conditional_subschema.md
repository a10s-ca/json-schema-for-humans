{% if schema.kw_if %}
    {% set first_property =  schema.kw_if | get_first_property %}
    {% if schema.kw_then %}
Si ({{ first_property.property_name }} = {{ first_property.const_value | python_to_json }}) alors les propriétés suivantes sont obligatoires
{% set required_props = schema.kw_then.required %}
{% if required_props %}
* {{ required_props | join('\n* ') }}
{% endif %}
    {% endif %}
    {% if schema.kw_else %}
Sinon ({{ first_property.property_name }} ≠ {{ first_property.const_value | python_to_json }}) alors les propriétés suivantes sont obligatoires
{% set required_props = schema.kw_else.required %}
{% if required_props %}
* {{ required_props | join('\n* ') }}
{% endif %}
    {% endif %}
{% endif %}
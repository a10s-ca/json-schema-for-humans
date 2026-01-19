{% if schema.kw_if %}
Condition particulière:
    {% set first_property = schema.kw_if | get_first_property %}
    {% if schema.kw_then %}
si ({{ first_property.property_name }} = {{ first_property.const_value | python_to_json }}) alors :

{% set required_props = schema.kw_then.required_properties %}
{% if required_props %}
- Les propriétés suivantes sont obligatoires :

{% for prop in required_props %}
    * {{ prop }}
{% endfor %}
{% endif %}
{% if schema.kw_then.properties %}
{% for prop_name, prop_node in schema.kw_then.properties.items() %}
    {% if prop_node.kw_enum %}
- `{{ prop_name }}` doit être l’une des valeurs suivantes :

{% for val in prop_node.kw_enum.array_items %}
    * {{ val.literal_str }}
{% endfor %}
    {% endif %}
    {% if prop_node.kw_pattern %}
- `{{ prop_name }}` doit respecter le pattern : `{{ prop_node.kw_pattern.literal_str }}`

    {% endif %}
{% endfor %}
{% endif %}
    {% endif %}
    {% if schema.kw_else %}
Sinon ({{ first_property.property_name }} ≠ {{ first_property.const_value | python_to_json }}) alors :

{% set required_props = schema.kw_else.required_properties %}
{% if required_props %}
- Les propriétés suivantes sont obligatoires :

{% for prop in required_props %}
    * {{ prop }}
{% endfor %}
{% endif %}
{% if schema.kw_else.properties %}
{% for prop_name, prop_node in schema.kw_else.properties.items() %}
    {% if prop_node.kw_enum %}
- `{{ prop_name }}` doit être l’une des valeurs suivantes :

{% for val in prop_node.kw_enum.array_items %}
    * {{ val.literal_str }}
{% endfor %}
    {% endif %}
    {% if prop_node.kw_pattern %}
- `{{ prop_name }}` doit respecter le pattern : `{{ prop_node.kw_pattern.literal_str }}`

    {% endif %}
{% endfor %}
{% endif %}
    {% endif %}
{% endif %}
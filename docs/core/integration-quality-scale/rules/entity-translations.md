---
title: "Entities have translated names"
related_rules:
  - has-entity-name
  - entity-device-class
  - icon-translations
  - exception-translations
---
import RelatedRules from './_includes/related_rules.jsx'

## Reasoning

Home Assistant is used by people all over the world.
To also make it easier for non-English speakers to use Home Assistant, it is important that entities have translated names.
This makes it easier for people to understand what the entity is.

## Example implementation

In this example, the sensor has the name "Phase voltage" in English.
Combined with the device name, this entity will name itself "My device Phase voltage".

`sensor.py`:
```python {5} showLineNumbers
class MySensor(SensorEntity):
    """Representation of a sensor."""

    _attr_has_entity_name = True
    _attr_translation_key = "phase_voltage"

    def __init__(self, device_id: str) -> None:
        """Initialize the sensor."""
        self._attr_device_info = DeviceInfo(
            identifiers={(DOMAIN, device_id)},
            name="My device",
        )
```

`strings.json`:
```json {5} showLineNumbers
{
    "entity": {
        "sensor": {
            "phase_voltage": {
                "name": "Phase voltage"
            }
        }
    }
}
```

:::info
If the entity's platform is either `binary_sensor`, `number`, `sensor`, or `update` and it has a device class set, and you want the entity to have the same name as the device class, you can omit the translation key because the entity will then automatically use the device class name.
:::

## Additional resources

More information about the translation process can be found in the [translation](/docs/internationalization/core) documentation, it also contains information about the [entity translations](/docs/internationalization/core#name-of-entities).
More information about entity naming can be found in the [entity](/docs/core/entity#has_entity_name-true-mandatory-for-new-integrations) documentation.

## Exceptions

There are no exceptions to this rule.

## Related rules

<RelatedRules relatedRules={frontMatter.related_rules}></RelatedRules>
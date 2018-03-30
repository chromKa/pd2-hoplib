# HopLib

Collection of functions and useful tools, currently mostly about retrieving information about units.

## Classes

### NameProvider

Provides names based on a tweak_data id

#### Translating unit names

The English localization file does not contain every existing unit name, as the NameProvider constructs most of the names from the unit's tweak_table id. If you want to translate a unit name that is not part of the English localization, you can simply add it to your localization file by constructing the key like ``unit_name_TWEAKTABLEID`` (or ``unit_name_TWEAKTABLEID_LEVELID`` if the unit should have a different name depending on the heist played).

### UnitInfoManager

Can be used to return information about a unit. Unit infos are created upon request (i.e. a call to ``get_info``) or by HopLib in certain cases.  
The following functions can be called on the active ``UnitInfoManager`` instance, which can be retrieved by calling ``HopLib:unit_info_manager()``:

- ``UnitInfoManager:all_infos()`` Returns a table containing all unit infos.
- ``UnitInfoManager:get_info(unit, [u_key])`` Returns the information about ``unit`` (creates it if it doesn't have it yet).
- ``UnitInfoManager:get_user_info(unit, [u_key])`` Returns the user of ``unit`` (shortcut for ``UnitInfoManager:get_info(unit):user()``).
- ``UnitInfoManager:clear_info(unit, [u_key])`` Clears the information about ``unit``.

Providing the optional ``u_key`` skips the function's internal ``unit:key()`` which might be useful if the unit has already been deleted but you have its key.

#### UnitInfo

The ``UnitInfoManager`` creates and returns ``UnitInfo`` objects, which contain various infos about the unit.  
The following functions can be called on a ``UnitInfo`` retrieved from the ``UnitInfoManager``.

- ``UnitInfo:unit()`` Returns the unit.
- ``UnitInfo:key()`` Returns the unit key.
- ``UnitInfo:id()`` Returns the unit id.
- ``UnitInfo:type()`` Returns the type of the unit. Possible values are ``"player"``, ``"npc"``, ``"projectile"`` and ``"sentry"``.
- ``UnitInfo:sub_type()`` Returns the sub type type of the unit (if available), depending on the main type. Possible values are ``"local_player"``, ``"remote_player"``, ``"team_ai"``, ``"joker"`` and ``"civilian"``.
- ``UnitInfo:name()`` Returns the name of the unit.
- ``UnitInfo:nickname()`` Returns the nickname of the unit (used for jokers and sentries). If it doesn't have one, returns the same as ``UnitInfo:name()``.
- ``UnitInfo:owner()`` Returns the ``UnitInfo`` of the unit owner (used for jokers and sentries).
- ``UnitInfo:user()`` Returns the ``UnitInfo`` of the unit user (currently only used for projectiles). If it doesn't have one, returns itself.
- ``UnitInfo:damage()`` Returns the amount of damage the unit has dealt.
- ``UnitInfo:kills()`` Returns the number of kills the unit made.
- ``UnitInfo:peer()`` Returns the peer object if the unit is of type ``"player"``.
- ``UnitInfo:level()`` Returns the level if the unit is of type ``"player"``.
- ``UnitInfo:rank()`` Returns the infamy rank if the unit is of type ``"player"``.
- ``UnitInfo:color_id()`` Returns the color id of the unit.
- ``UnitInfo:is_special()`` Returns ``true`` if the unit is a special enemy.
- ``UnitInfo:is_boss()`` Returns ``true`` if the unit is a boss type enemy.
- ``UnitInfo:is_female()`` Returns ``true`` if the unit is female (currently only works on enemies and civilians).

## Hooks

HopLib provides the following hooks:

- ``HopLibOnUnitDamaged`` with parameters ``(unit, damage_info)``
- ``HopLibOnUnitDied`` with parameters ``(unit, damage_info)``
- ``HopLibOnEnemyConverted`` with parameters ``(unit, player_unit)``
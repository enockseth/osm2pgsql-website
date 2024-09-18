---
chapter: 21
appendix: B
title: Lua Library for Flex Output
functions:
    - name: clamp
      synopsis: osm2pgsql.clamp(VALUE, MIN, MAX)
      description: |
        Return VALUE if it is between MIN and MAX, MIN if it is smaller, or MAX
        if it is larger. All parameters must be numbers. If VALUE is `nil`,
        `nil` is returned.
      example: |
        osm2pgsql.clamp(2, 3, 4) ⟶ 3
    - name: has_prefix
      version: 1.4.0
      synopsis: osm2pgsql.has_prefix(STRING, PREFIX)
      description: |
        Returns `true` if the STRING starts with PREFIX. If STRING is `nil`,
        `nil` is returned.
      example: |
        osm2pgsql.has_prefix('addr:city', 'addr:') ⟶ true
    - name: has_suffix
      version: 1.4.0
      synopsis: osm2pgsql.has_suffix(STRING, SUFFIX)
      description: |
        Returns `true` if the STRING ends with SUFFIX. If STRING is `nil`,
        `nil` is returned.
      example: |
        osm2pgsql.has_suffix('tiger:source', ':source') ⟶ true
    - name: make_check_values_func
      synopsis: osm2pgsql.make_check_values_func(VALUES[, DEFAULT])
      description: |
        Return a function that will check its only argument against the list of
        VALUES. If it is in that list, it will be returned, otherwise the
        DEFAULT (or nil) will be returned.
      example: |
        local get_highway_value = osm2pgsql.make_check_values_func({
                'motorway', 'trunk', 'primary', 'secondary', 'tertiary'
        }, 'road')
        ...
        if object.tags.highway then
            local highway_type = get_highway_value(object.tags.highway)
            ...
        end
    - name: make_clean_tags_func
      synopsis: osm2pgsql.make_clean_tags_func(KEYS)
      description: |
        Return a function that will remove all tags (in place) from its only
        argument if the key matches KEYS. KEYS is an array containing keys,
        key prefixes (ending in `*`), or key suffixes (starting with `*`).
        The generated function will return `true` if it removed all tags,
        `false` if there are still tags left.
      example: |
        local clean_tags = osm2pgsql.make_clean_tags_func{'source', 'source:*', '*:source', 'note'}

        function osm2pgsql.process_node(node)
            if clean_tags(node.tags) then
                return
            end
            ...
        end
    - name: split_string
      version: 1.4.0
      synopsis: osm2pgsql.split_string(STRING[, DELIMITER])
      description: |
        Split STRING on DELIMITER (default: ';' (semicolon)) and return an
        array table with the results. Items in the array will have any
        whitespace at beginning and end removed. If STRING is `nil`, `nil` is
        returned.
      example: |
        local opening_hours = osm2pgsql.split_string(object.tags.opening_hours)
    - name: split_unit
      version: 1.4.0
      synopsis: osm2pgsql.split_unit(STRING, DEFAULT_UNIT)
      description: |
        Split STRING of the form "VALUE UNIT" (something like "10 mph" or
        "20km") into the VALUE and the UNIT and return both. The VALUE must
        be a negative or positive integer or real number. The space between
        the VALUE and UNIT is optional. If there was no unit in the string,
        the DEFAULT_UNIT will be returned instead. Return `nil` if the STRING
        doesn't have the right pattern or is `nil`.
      example: |
        value, unit = osm2pgsql.split_unit(object.tags.maxspeed, 'km/h')
    - name: trim
      version: 1.4.0
      synopsis: osm2pgsql.trim(STRING)
      description: |
        Return STRING with whitespace characters removed from the beginning
        and end. If STRING is `nil`, `nil` is returned.
      example: |
        local name = osm2pgsql.trim(object.tags.name)
    - name: way_member_ids
      synopsis: osm2pgsql.way_member_ids(RELATION)
      description: |
        Return an array table with the ids of all way members of RELATION.
      example: |
        function osm2pgsql.select_relation_members(relation)
            if relation.tags.type == 'route' then
                return { ways = osm2pgsql.way_member_ids(relation) }
            end
        end
---

The flex output includes a small library of useful Lua helper functions.
All functions are in the `osm2pgsql` namespace.

These functions are available on the flex output, they cannot be used in
the Lua tag transformations of the pgsql output.
{:.note}

{% for func in page.functions -%}
<table class="lib">
    <tbody>
        <tr class="lib-name"><th>Name</th><td>{{ func.name }}{%- if func.version -%} <span class="version" style="font-weight: normal;">(available from version {{ func.version }})</span>{%- endif -%}</td></tr>
        <tr class="lib-syno"><th>Synopsis</th><td>{{ func.synopsis }}</td></tr>
        <tr class="lib-desc"><th>Description</th><td>{{ func.description }}</td></tr>
        <tr class="lib-exam"><th>Example</th><td>{{ func.example }}</td></tr>
    </tbody>
</table>
{%- endfor -%}


# Installation

```bash
git clone git@github.com:tacman/twig-tree-tag-demo && cd twig-tree-tag-demo
composer install
symfony server:start -d
symfony open:local
```

This repo is a minimal application for the tree tag, it can be recreated in minutes

```bash
symfony new --webapp twig-tag-bug && cd twig-tag-bug
composer req tacman/twig-tree-tag
bin/console make:controller AppController
cat > templates/app/index.html.twig << 'END'
{% extends 'base.html.twig' %}

{% block title %}Hello AppController!{% endblock %}

{% block body %}
    {% set food = [
        {   name: 'fruits', 
            children: [{name: 'apple'},{name:'banana'}]        },
        {   name: 'veggies',
            children: [
            {name: 'peas'},
            {name: 'carrots'}
        ]
        }
    ] %}
    <h1>Food Tree</h1>
    {% tree item in food %}
        {% if treeloop.first %}<ul>{% endif %}
        <li>
            {{ item.name }}
            {% subtree item.children|default([]) %}
        </li>
        {% if treeloop.last %}</ul>{% endif %}
    {% endtree %}

{% endblock %}
END
```

Add to services.yaml

```yaml
services:
  
    
    twig.tree:
        class: JordanLev\TwigTreeTag\Twig\Extension\TreeExtension
        tags:
            - { name: twig.extension }

```


# 

```bash
symfony new --webapp twig-tag-bug && cd twig-tag-bug
composer req tacman/twig-tree-tag
bin/console make:controller AppController
cat > templates/app/index.html.twig << 'END'

```

Add to services.yaml

```yaml
services:
  
    
    twig.tree:
        class: JordanLev\TwigTreeTag\Twig\Extension\TreeExtension
        tags:
            - { name: twig.extension }

```


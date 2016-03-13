# Updating to [r16](https://code.google.com/p/django-cron/source/detail?r=16) or higher - READ THIS FIRST #
If you are updating to [r16](https://code.google.com/p/django-cron/source/detail?r=16) or higher from previous versions, please note that you will need to **update your cron.py files**

you will need to change your old imports:
```
    # Old and no longer works
    from django_cron.base import cron
```

to

```
    # new version: fixes namespace problems
    from django_cron import cronScheduler as cron
```

This change was to resolve an ugly namespace problem
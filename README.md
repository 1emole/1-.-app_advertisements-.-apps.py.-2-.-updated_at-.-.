from django.apps import AppConfig

class YourAppConfig(AppConfig):
    name = 'app_advertisements'
    verbose_name = 'Объявления'

    from django.contrib import admin
    from .models import YourModel
    from django.utils import timezone

    class YourModelAdmin(admin.ModelAdmin):
        list_display = ('title', 'created_at', 'updated_at', 'display_updated_at')

        def display_updated_at(self, obj):
            if obj.updated_at.date() == timezone.now().date():
                return timezone.now().strftime('Сегодня в %H:%M')
            return obj.updated_at.strftime('%d-%m-%Y %H:%M')

        display_updated_at.short_description = 'Обновлено'

    admin.site.register(YourModel, YourModelAdmin)

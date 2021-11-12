ckanext-solr-query-config
#################

*ckanext-solr-query-config* ist eine CKAN Extension und erlaubt es CKAN Parameter, die an Solr gesendet werden, zu überschreiben.
*ckanext-solr-query-config* war ursprünglich Teil des größeren ckanext-discovery Plugins und kann jetzt als eigenständiges Plugin genutzt werden.

This Repo currently is only in german language available. Feel free to submit translations.

System-Voraussetzungen
======================

Getestet wurde das Plugin mit CKAN 2.9.
Andere Versionen wurden nicht getestet. Feedback zur Funktionalität mit anderen Versionen sind herzlich Willkommen.

Installation
============

Aktivieren der CKAN-Umgebung::

    . /usr/lib/ckan/default/bin/activate

Installation des Plugins::

    pip install -e git+https://github.com/ondics/ckanext-solr-query-config#egg=ckanext-solr-query-config

Zum Installieren einer bestimmten Version::

    pip install -e git+https://github.com/ondics/ckanext-solr-query-config@v1.0.0#egg=ckanext-solr-query-config

Hinzufügen von ``solr-query-config`` zur Liste der aktiven Plugins in der CKAN Konfigurations INI::
    
    plugins = ... solr_query_config

CKAN neu starten::

    sudo service apache2 restart

oder::

    sudo supervisorctl restart ckan-uwsgi:


Konfiguration
=============

solr-query-config ermöglicht es die Parameter, die CKAN an Solr sendet, durch Einträge in CKANs Konfigurations INI einfach zu überschreiben.
Es kann entweder ein Default Wert für einen Parameter angeben werden (wird standardmäßig in Anfragen verwendet, in denen der Parameter nicht explizit gesetzt ist)
oder es kann ein Wert forciert werden.

Um einen Default Wert anzugeben, wird folgender Code dem Parameternamen vorangestellt::
``ckanext.solr_query_config.default.`` z.B.::

    # Per Default wird nach dem Metadaten Modifikations Zeitstempel sortiert::
    ckanext.solr_query_config.solr.default.sort = metadata_modified asc

Auf ähnliche Weise kann ein Wert mit folgendem Präfix forciert werden::
``ckanext.solr_query_config.force.`` z.B.::

    # Es wird immer ein benutzerdefinierter Solr query handler verwendet:
    ckanext.solr_query_config.solr.force.defType = my_special_query_handler

Nur die Solr Parameter, die von der package_search_ API akzeptiert werden, können auf diese Weise eingestellt werden.

Credits
=======

Dank geht an die Repo-Ersteller

    CKAN_
    SOLR_
    ckanext-discovery_

Lizenz
=======

Distributed in der the GNU Affero General Public License. See the file
``LICENSE`` for details.

Autor
=====

Copyright (C) 2021 Ondics GmbH
https://ondics.de


.. _CKAN: https://ckan.org
.. _SOLR: https://solr.apache.org/
.. _configuration INI: https://docs.ckan.org/en/latest/maintaining/configuration.html#ckan-configuration-file
.. _package_search: https://docs.ckan.org/en/latest/api/index.html#ckan.logic.action.get.package_search
.. _template snippet: https://docs.ckan.org/en/latest/theming/templates.html#snippets
.. _ckanext-discovery: https://github.com/stadt-karlsruhe/ckanext-discovery

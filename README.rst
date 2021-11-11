ckanext-solr-query-config
#################

*ckanext-solr-query-config* war ursprünglich Teil des größeren ckanext-discovery Plugins und kann jetzt als eigenständiges Plugin genutzt werden.
Getestet wurde das Plugin mit CKAN 2.9.
Andere Versionen wurden nicht getestet. Feedback zur Funktionalität mit anderen Versionen sind herzlich Willkommen.

Installation
============

Aktivieren Sie zuerst die CKAN-Umgebung::

    . /usr/lib/ckan/default/bin/activate

Dann installieren Sie die das dieses Plugin::

    pip install -e git+https://github.com/ondics/ckanext-solr-query-config#egg=ckanext-solr-query-config

Wenn Sie eine bestimmte Version installieren möchten, können Sie es im wie folgt angeben:

    pip install -e git+https://github.com/ondics/ckanext-solr-query-config@v0.1.1#egg=ckanext-solr-query-config

Fügen Sie ``solr-query-config`` zu Ihrere Liste aktiver Plugins in der CKAN Konfigurations INI hinzu::
    
    plugins = ... solr_query_config

und starten Sie CKAN neu::

    sudo service apache2 restart

oder

    sudo supervisorctl restart ckan-uwsgi:


Konfiguration
=============

solr-query-config ermöglicht es Ihnen die Parameter, die CKAN an Solr sendet, durch Einträge in CKANs Konfigurations INI einfach zu überschreiben.
Sie können einfach einen Default Wert für einen Parameter angeben (dieser Default Wert wird nur in Anfragen genutzt, in denen dieser Parameter noch nicht gesetzt ist)

Um einen Default Wert anzugeben, stellen Sie folgenden Code dem Parameternamen voran::
``ckanext.solr_query_config.default.`` z.B.::

    # Per Default wird nach dem Metadaten Modifikations Zeitstempel sortiert::
    ckanext.solr_query_config.solr.default.sort = metadata_modified asc

Auf ähnliche Weise kann ein Wert mit folgendem Präfix forciert werden::
``ckanext.solr_query_config.force.`` z.B.::

    # Es wird immer ein benutzerdefinierter Solr query handler verwendet:
    ckanext.solr_query_config.solr.force.defType = my_special_query_handler

Bitte beachten Sie, dass nur die Solr Parameter, die von der package_search_ API akzeptiert werden, so eingestellt werden können.


Lizenz
=======
Copyright (C) 2021 Ondics GmbH (www.ondics.de)

Distributed in der the GNU Affero General Public License. See the file
``LICENSE`` for details.


.. _CKAN: http://ckan.org
.. _configuration INI: http://docs.ckan.org/en/latest/maintaining/configuration.html#ckan-configuration-file
.. _package_search: http://docs.ckan.org/en/latest/api/index.html#ckan.logic.action.get.package_search
.. _More Like This: https://cwiki.apache.org/confluence/display/solr/MoreLikeThis
.. _MoreLikeThisHandler: https://cwiki.apache.org/confluence/display/solr/MoreLikeThis#MoreLikeThis-ParametersfortheMoreLikeThisHandler
.. _term vector storage: https://cwiki.apache.org/confluence/display/solr/Field+Type+Definitions+and+Properties#FieldTypeDefinitionsandProperties-FieldDefaultProperties
.. _template snippet: http://docs.ckan.org/en/latest/theming/templates.html#snippets


# DHIS version 2.38 Release Note

---

## ANALYTICS FEATURES

**New Line Listing app:** A new Line Listing app is developed for compatibility with DHIS 2.38 and will be released soon via the App Hub. This new application is a massive improvement for producing line lists of tracked entities in DHIS2 over the event reports application. The new line listing application replicated all of the line listing functionalities of the event reports app, and it has a completely new, much improved user experience that makes it much easier for users to make a line list of tracked entities. It also includes many new features. A list of some of the key new features:
* Visualizing multiple repeating events: You are now able to produce a line list that can display data from multiple repeating stage for a single tracked entity. You can specify how many repeated stages you would like to see data from. This is useful for many health and education programs by enabling the visualization of data captured repeatedly over time for a single patient or student.  
[Screenshot 1](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38repeatingevent.png) | [Screenshot 2](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38repeatingevent2.png)
* New tracker specific period dimensions: In the new Line Listing application you can produce a linelist showing enrollment date, event date, and/or incident date. These can be each defined, sorted, and shown together in a single line list.  
[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38linelisttimedemensions.png) 
* Created by and Last updated by: This allows you to see the user name of the user that has either created the enrollment or the user that has last updated the data for the tracked entity.

[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38_linelist_2.png) 

*Note:* Program indicators that have an analytics_period_start and/or an analytics_period_end dates defined will not be displayed in the line listing application.  

**Catchment areas for org units:** DHIS2 now supports multiple geometries (points and shapes) to be stored for organisation units. This allows for displaying multiple polygons, such as catchment areas, in a map. These can be viewed in the Maps app and selected from the org unit selector. This means that system administrators can upload catchment areas for their facilities, community health posts, schools, hospitals, etc and visualize any data by catchment area.

[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38_catchment_area.png) | [Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-235/analysing-data/maps.html)

**Support for Google Earth Engine Building/Structures Layer:** In the maps app users can now see structure outlines as identified by Google's Open Building dataset. This data set includes 516M buildings (64% of the African continent). It is useful for population estimation, urban planning, outreach and health programs, and humanitarian response for example. The number of buildings can be shown by catchment or org unit boundaries. The performance for EE layers is greatly improved through the use of web workers.

[Screenshot 1](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38_structures_1.png) | [Screenshot 2](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/2.38_structures_2.png) | [Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-235/analysing-data/maps.html) 

**Vector tiles support in Maps:** The Maps app now supports vector tiles for external base maps. This leads to better performance when loading large maps, better maps resolution and a seamless zoom experience. The default base map to display can now be defined as a system setting. 

[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/maps_vector_tiles.png) 

**Indicator aggregation type override:** An indicator expression can now specify an aggregation type, overriding the default type assigned to a data element. For example if a data element has aggregation type SUM, an indicator may also report the value by AVERAGE or COUNT.  

_Example expression in indicators: #{EX2jBdKe4Yq}.aggregationType(COUNT)_ Description: ER Teachers Trained.aggregationType(COUNT) 

[Docs](https://docs.dhis2.org/en/full/use/user-guides/dhis-core-version-236/dhis2-user-manual.html#manage_indicator)

**Indicator min and max date:** A min and/or max date may be specified for fetching a data element for an indicator. This can be useful when data semantics change from time to time requiring different calculations for the same result. It allows an indicator to report consistently across these changes by changing the way the indicator is calculated through time. The *period offset* function (since 2.36) can also be used to include data from a different period in an indicator expression.

_Example minDate and maxDate expression in indicators: #{EX2jBdKe4Yq}.minDate(2021-1-1).maxDate(2021-6-30)_ Description: ER Teachers Trained.minDate(2021-1-1).maxDate(2021-6-30) -> Only values between Jan. 1, 2021 and June 30, 2021 for ER Teachers Trained will be used in the indicator calculation. 

_Example periodOffset expression in indicators: #{EX2jBdKe4Yq} + #{EX2jBdKe4Yq}.periodOffset(-1) + #{EX2jBdKe4Yq}.periodOffset(-2)_ Description: ER Teachers Trained + Description: ER Teachers Trained +  ER Teachers Trained.periodOffset(-1) + ER Teachers Trained.periodOffset(-2) -> Sum of the ER Teachers Trained over the last three months relative to the period selection in the analytics app being used to visualize this value. 

 [Docs](https://docs.dhis2.org/en/full/use/user-guides/dhis-core-version-236/dhis2-user-manual.html#manage_indicator)

**Indicator sub-expressions (for 2.38.1):** Indicators can count the number of organizational units where a data element compares in a specific way with a fixed value.

_Example subExpression expression in indicators: subExpression( if (#{vq2q03TrNi} > 100, 1, 0) )_ Description: subExpression(if(IDSR Malaria>100,1,0)) -> Counts the number of organizational units where more than 100 Malaria cases were reported within a given period defined in the analytics app being used to visualize this value.

 [Docs](https://docs.dhis2.org/en/full/use/user-guides/dhis-core-version-236/dhis2-user-manual.html#manage_indicator)

---

## TRACKER AND EVENT FEATURES

**Tracker program working list improvements:** Working lists for tracker programs has been expanded to be similar to those of event working lists. The Capture app now allows working lists to be configured, saved, shared, deleted and updated through the user interface. 

[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/Working_list.png) | [Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/capture.html#capture_views) | [Jira](https://jira.dhis2.org/browse/DHIS2-9275)

**Translation of program rule actions:** The content of program rule actions, the "static text" that is being visualized to the users, can be translated and shown in Tracker programs. This applies to both the Tracker Capture and Capture apps.

[Jira](https://jira.dhis2.org/browse/DHIS2-12137)

**Description and URLs for data elements and tracked entity attributes:** Description and URL set on these data items are displayed in a popover. This popover can be accessed by clicking the information icon that displays after the data element name. The description is set in the Maintenance app and can be used to provide more information about what to capture for the data item.

[Screenshot](https://s3.eu-west-1.amazonaws.com/content.dhis2.org/releases/screenshots/38/Capture_DE_description.png) | [Jira](https://jira.dhis2.org/browse/DHIS2-5345)

**New org unit component in Capture app:** The org unit component used in Capture app has been replaced with the redesigned org unit from the *d2-ui* library.

[Jira](https://jira.dhis2.org/browse/DHIS2-11806)

**Support for GS1 Data Matrix:** GS1 Data Matrix is used for pharmaceutical and health commodity bar coding and will support supply chain use cases. Given a field value formatted with the GS1 data matrix standard and a string key from the GS1 application identifiers, there is now support for program rules extracting the values from this delimited text and assigning values to their designated fields. This is implemented in Tracker Capture, Capture and the Android Capture app.

[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/configuring-the-system/programs.html#program_rules_operators_functions) | [Jira](https://jira.dhis2.org/browse/DHIS2-12353)

**Data/Value type for program rule variable:** For the program rule variables with source type *Calculated value*, the Maintenance app will offer the user to assign a value type. The default value type for calculated values will be text. For all other program rule variable source types, the value type selection should not be visible, as the variable will inherit the type from the underlying data element or tracked entity attribute.

[Jira](https://jira.dhis2.org/browse/DHIS2-12096)

**Programs can remain open after attribute option end date:** A specified program can remain open after its related attribute option is closed.

[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/configuring-the-system/programs.html#tracker_enter_programs_details) | [Jira](https://jira.dhis2.org/browse/DHIS2-12118)

**Capture app continuously released:** The Capture app will from now on be released continuously on the App Hub. Bug fixes and new features will be made available for download and can be integrated at the time they are needed, without upgrading the entire DHIS2 application. The first updated version of the Capture app will become available on the App Hub shortly after the 2.38.0 release. The App Hub is accessed through the App management app.

**Tracker features in Capture App:** In addition to the Tracker functionality that was added in 2.37 for closed beta testing, additional functionality has been added. The new functionality can be tested by installing the updated Capture app from App Hub, and opting in to using the tracker features in the Capture app. Only superusers or users with access to changing the program metadata will have the opt-in functionality available. The new tracker functionality that can be tested by opting in is listed here:

* TEI profile widget: On the enrollment dashboard, you can view the tracked entity instance profile widget. Inside the profile widget you can view the key attributes values. Click the Edit button to make changes to the tracked entity instance profile. Editing the profile opens a dialog where the profile attributes can be changed.  
[Jira](https://jira.dhis2.org/browse/DHIS2-10946)
* Scheduling event widget form: Instead of reporting an event the user can select to schedule an event later. This is done with a scheduled date. The dialog will open with a suggested scheduled date, and this date is determined by a set of rules from program stage configuration and program configuration.  
[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/capture.html#schedule-event-widget-form) | [Jira](https://jira.dhis2.org/browse/DHIS2-11861)
* Quick actions in Enrollment Dashboard: The quick actions widget offers shortcuts for frequently used actions for the current enrollment, including creating an event and scheduling an event.  
[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/capture.html#quick-actions) | [Jira](https://jira.dhis2.org/browse/DHIS2-11953)
* "Add new" for Completed enrollments in Enrollment Widget: There can only be one active enrollment at a time, but if all enrollments is completed, there will  be an option to enroll the TEI in the program again in the enrollment widget, f the program allows more than one enrollment per TEI. If program does not allow more than one enrollment, the add new button will be disabled.  
[Jira](https://jira.dhis2.org/browse/DHIS2-12141)
* Re-enroll an existing tracked entity instance: By having a tracked entity instance selected in the locked selector and selecting a different program, you can now re-enroll existing TEIs into other programs. The registration page will be pre-filled with any overlapping tracked entity attribute values.    
[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/capture.html#re-enroll-an-existing-tracked-entity-instance)  | [Jira](https://jira.dhis2.org/browse/DHIS2-12141)

---

## PLATFORM FEATURES

**Version check notifications:** A new DHIS 2 version check notification service is introduced, which will send notifications in the form of DHIS 2 system inbox messages when newer versions of DHIS 2 has become available. This includes major and patch versions. This is useful to encourage sysadmins to upgrade DHIS 2 to keep their instance secure and up to date.

[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/configuring-the-system/system-settings.html#system_update_notification_settings) | [Jira](https://jira.dhis2.org/browse/DHIS2-9897)

**GeoJSON metadata attributes:** GeoJSON is now supported as value type for metadata attributes. This allows you to store any number of GeoJSON documents, e.g. for organisation units.

[Docs]() | [Jira](https://jira.dhis2.org/browse/DHIS2-12328)

**ADX export:** The import/export app now allows data import and export using the ADX data format.

[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/maintaining-the-system/importexport-app.html) | [Jira](https://jira.dhis2.org/browse/DHIS2-4978)

**Configurable log level:** Logging levels can now be configured in the `dhis.conf` configuration file on the package level. This means that you can specify the log level to output for specific frameworks and modules within DHIS 2 directly in the DHIS 2 configuration file.

[Docs](https://docs.dhis2.org/en/manage/performing-system-administration/dhis-core-version-master/installation.html#log-level-configuration) | [Jira](https://jira.dhis2.org/browse/DHIS2-11898)

**Account disable notifications:** When automatically disabling users through the disable users schedulded job, an email notification can be sent to the relevant user. The number of days before the notification can be defined in the job configuration. This is useful to give users a chance to log in before their account is disabled.

[Docs](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-238/maintaining-the-system/scheduling.html) | [Jira](https://jira.dhis2.org/browse/DHIS2-11589)

**Data value set input ID scheme:** Input identifier schemes is now supported for the data value sets API endpoint, allowing you to import data using the code field to reference metadata.

[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/data.html) | [Jira](https://jira.dhis2.org/browse/DHIS2-9822)

**Group sets short name:** The indicator group set and category option group sets now have short name properties, which allows for precise and UI-friendly rendering. The short names are now used as column names in resource tables instead of names.

[Jira](https://jira.dhis2.org/browse/DHIS2-7317)

**Analytics cache handling:** The cache for analytics data is now automatically flushed when the analytics database tables are updated. This ensures that analytics queries read the latest data from the analytics data and reduce the time lag between analytics tables being updated and data appearing in data visualizations.  

[Jira](https://jira.dhis2.org/browse/DHIS2-12072)

---

### PLATFORM API FEATURES

**Data store improvements:** The data store API has received numerous improvements to make it a fully-fledged data store and more useful to web apps and other clients.

* **Field filtering:** Allows you to return only specific keys and values of entries in the data store using the `fields` parameter. Works similar to fields filtering in the metadata API. The filtering takes place at the namespace level and is useful when a client needs to list many entries with specific keys/values in a single query.  
[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/data-store.html#query-api) | [Jira](https://jira.dhis2.org/browse/DHIS2-12154)
* **Paging:** In query responses, paging is supported and enabled by default. You can specify paging explicitly with the `page` and `pageSize` parameters. Paging is useful to work with namespaces with high numbers of entries.  
[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/data-store.html#query-api) | [Jira](https://jira.dhis2.org/browse/DHIS2-12329)
* **Entry filtering:** Allows you to match and filter entries in a namespace based on a variety of operators, such as `eq`, `lt`, `le`, `gt`, `ge`, `like`, `null`, using the `filter` parameter. Works similar to object filtering in the metadata API. The filtering is useful when a client wants to list many entries which match one or many criteria.  
[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/data-store.html#filtering-entries) | [Jira](https://jira.dhis2.org/browse/DHIS2-12331)
* **Sorting:** Allows you to sort entries in a namespace ascending or descending based on a specific key/value using the `order` parameter.  This is useful when clients have specific requirements for sorting a list of entries.  
[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/data-store.html#sorting-results) | [Jira](https://jira.dhis2.org/browse/DHIS2-12330)

**Request logging:** Clients of the API can now submit a value with the `X-Request-ID` HTTP header which is included in all log statements. This is useful when looking at DHIS 2 logs and trying to understand which client/app made a request, for example when debugging an issue which applies to a specific installation of an Android app on a phone.

[Docs](https://docs.dhis2.org/en/manage/performing-system-administration/dhis-core-version-238/installation.html#log-configuration) | [Jira](https://jira.dhis2.org/browse/DHIS2-6494)

**Cancel analytics table jobs:** You can now cancel (stop) analytics tables jobs while they are running. This is useful in order to stop long-running jobs without having to wait for them to complete.

[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/scheduling.html#request-cancelling-a-running-jobs) | [Jira](https://jira.dhis2.org/browse/DHIS2-6314)

**Metadata proposal workflow:** The new metadata proposal workflow endpoint allows for a workflow of metadata changes. The stages include proposing, accepting, opposing, adjusting and rejecting a metadata change. This is useful e.g. for facility registries where changes to organisation units must be managed.

[Docs](https://docs.dhis2.org/en/develop/using-the-api/dhis-core-version-238/metadata.html#webapi_metadata_proposal_workflow) | [Jira](https://jira.dhis2.org/browse/DHIS2-4828)

---

## RELEASE INFO

|Release Information|Link|
| --- | --- |
|Download release and sample database|https://www.dhis2.org/downloads|
|Documentation|[https://docs.dhis2.org](https://docs.dhis2.org/)|
|Upgrade notes|[Upgrade notes on GitHub](https://github.com/dhis2/dhis2-releases/blob/master/releases/2.38/README.md)|
|Full list of features and bugs|[Release Note](https://github.com/dhis2/dhis2-releases/blob/master/releases/2.38/ReleaseNote-2.38.0.md)|
|Source code on Github|https://github.com/dhis2|
|Demo instance|https://play.dhis2.org/2.38/|
|Docker image|`docker pull dhis2/core:2.38.0`|
|Docker Hub images|https://hub.docker.com/r/dhis2/core|
|Community forum|https://community.dhis2.org/|

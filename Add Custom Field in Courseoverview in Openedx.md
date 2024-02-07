# Add Custom Field in Courseoverview in Openedx

- Add Field in Model, and Migrate the Model
```
openedx>core>djangoapps>content>course_overviews>models.py>CourseOverview
```

- Make Front-End
```
cms>templates>settings.html
```

- Add Required JS in JS Files

```
1. cms>static>js>views>settings>main.js

2. cms>static>js>models>settings>course_details.js
```

- Make Field in Mongodb
```
xmodule>course_block.py>CourseFields
```

- Save Changed Data From CMS Settings
```
openedx>core>djangoapps>model>course_details.py>CourseDetails>{initialize the field}

openedx>core>djangoapps>model>course_details.py>CourseDetails>populate>{course_details.fields = block.field}

openedx>core>djangoapps>model>course_details.py>CourseDetails>update_from_json>save the data in mongo

```

- If Needed of Sending Contexts in CMS Settings You Can Send Form Below File:

```
cms>djangoapps>contentstore>utils.py>get_course_settings
```

- To See Changes in Mysql Change in Below File 

```
openedx>core>djangoapps>content>course_overviews>models.py>CourseOverview>_create_or_update

```

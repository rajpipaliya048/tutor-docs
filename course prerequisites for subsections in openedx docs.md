# course prerequisites openedx for subsections

- enable this flag in lms.yml and studio.yml
```
# Milestones application flag
'MILESTONES_APP': True,

# Prerequisite courses feature flag
'ENABLE_PREREQUISITE_COURSES': true,
```

- In studio advanced settings enable this feature to true
```
Enable subsection prerequisites = true
```

### For Entrance exam enable this feature in lms.yml and studio.yml
```
# Entrance exams feature flag
'ENTRANCE_EXAMS': True,
```

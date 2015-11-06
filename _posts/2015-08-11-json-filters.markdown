---
layout:     post
title:      "Json Filters"
subtitle:   "Json Filters"
date:       2015-08-11 12:00:00
author:     "Sriram Mantha"
---

#JSON Filters
In situations where you would like to filter properties from getting serialized dynamically per request Jackson provides a way through JsonFilter's
http://wiki.fasterxml.com/JacksonFeatureJsonFilter

Here is an example code to create a dynamic filter

``` java
//Your custom logic can go here
SimpleBeanPropertyFilter theFilter = new SimpleBeanPropertyFilter() {
            @Override
            protected boolean include(BeanPropertyWriter writer) {
                Annotation annotation = writer.getAnnotation(CustomAnnotation.class);
                //Custom logic. Return true if the bean property has to be serialized
                .....

            }
};
```

``` java
//Add the filter to the list of filters with id. In this case its "enableClientBasedFiltering"
FilterProvider filters = new SimpleFilterProvider().addFilter("dynamicFilter", theFilter);
objectMapper.setFilters(filters);
```

If the bean is tagged with JsonFilter Annotation example. @JsonFilter("myFilterId") , then Jackson calls the associated filter for evaluation per request

Jackson does throw an exception when filter is not found. You would have to ensure that the bean marked with JsonFilter annotation should  have the filter defined in the object mapper in its classpath
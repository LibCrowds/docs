LibCrowds anayses results in real-time

As each task is completed a webhook is sent off to an endpoint that handles
that type of task

!!! info
    Results analysis relies on the
    [pybossa-lc](https://github.com/LibCrowds/pybossa-lc) plugin being
    installed. If you're running your own instance of LibCrowds, see the
    [Setup](/setup/installation.md) guide.


## Z39.50

For Z39.50 projects, the results are analysed as follows:

### 1. Check if all answers are empty.

This means that no users were able to find suitable matches and no comments
were given. If tihs is the case, an empty value is stored against each answer
key and the analysis process ends.

#### Result

```json
{
  "control_number": "",
  "reference": "",
  "comments": ""
}
```

### 2. Check if the required match rate is met

If

2. Otherwise, a specified percentage of answers match. By default this is 60%,
which equates to, for example, at least 2 out of 3 or 3 out of 5 answers.
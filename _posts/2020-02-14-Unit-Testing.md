---
layout: post
title: Unit Testing
---
Before talking about what is unit testing, I still gonna be finishing off my implementation of python regular expression.
<img src="/img/posts/vrf.png" alt="vrf definition" align="center"/>
~~~
vrf_list = ["vrf" + s for s in text.strip().split("vrf") if s]
return_dict = {}
for vrf in vrf_list:
    #parse the VRF name from the definition line
    name_regex = re.compile(r"vrf\s+definition\s+(?P<name>\S+)")
    sub_dict = { }
    vrf_dict = {name_match.group("name"): sub_dict}
~~~
Pass static input to function and assert expected result is correct and catch small problems early.
~~~
from parse_model import parse_model_ios, parse_model_iosxr
#define a static input text
model_output =""
print(model_output)
model_data = parse_model_ios(model_ouput)
print(model_data)
#perform parsing,print structured data and validate
model_data = parse_model_ios(model_output)
print(model_data)
assert model_data == "CSR1000V"
~~~
Usually the output is a list. Use zip to merger list. So we can  just compare the output and the answer.
~~~
#easier than last solution
for model_output, model_answer in zip(model_output_list, model_answer_list):
    print(model_ouput)
    model_data = parse_model_iosxr(model_output)
    print(model_data)
    assert model_data == model_answer
~~~
Using pytest. Mainly check the length.  We use regular expression to extract and store them in dictionary or combinations of strings and lists. And we use pytest to see if our parsers work correctly. Next, we are going to use NAPALM

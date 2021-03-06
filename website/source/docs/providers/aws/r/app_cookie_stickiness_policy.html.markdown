---
layout: "aws"
page_title: "AWS: aws_app_cookie_stickiness_policy"
sidebar_current: "docs-aws-app-cookie-stickiness-policy"
description: |-
  Provides an application cookie stickiness policy, which allows an ELB to wed its stickiness cookie to a cookie generated by your application.
---

# aws\_app\_cookie\_stickiness\_policy

Provides an application cookie stickiness policy, which allows an ELB to wed its sticky cookie's expiration to a cookie generated by your application.

## Example Usage

```
resource "aws_elb" "lb" {
    name = "test-lb"
	availability_zones = ["us-east-1a"]
	listener {
	  instance_port = 8000
	  instance_protocol = "http"
	  lb_port = 80
	  lb_protocol = "http"
    }
}

resource "aws_app_cookie_stickiness_policy" "foo" {
	name = "foo_policy"
	load_balancer = "${aws_elb.lb.name}"
	lb_port = 80
	cookie_name = "MyAppCookie"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the stickiness policy.
* `load_balancer` - (Required) The name of load balancer to which the policy
  should be attached.
* `lb_port` - (Required) The load balancer port to which the policy
  should be applied. This must be an active listener on the load
balancer.
* `cookie_name` - (Required) The application cookie whose lifetime the ELB's cookie should follow.

## Attributes Reference

The following attributes are exported:

* `id` - The ID of the policy.
* `name` - The name of the stickiness policy.
* `load_balancer` - The name of load balancer to which the policy is attached.
* `lb_port` - The load balancer port to which the policy is applied.
* `cookie_name` - The application cookie whose lifetime the ELB's cookie should follow.

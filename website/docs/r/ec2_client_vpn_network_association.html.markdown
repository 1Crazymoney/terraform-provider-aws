---
layout: "aws"
page_title: "AWS: aws_ec2_client_vpn_network_association"
sidebar_current: "docs-aws-resource-ec2-client-vpn-network-association"
description: |-
  Provides network associations for AWS Client VPN endpoints.
---

# aws_ec2_client_vpn_network_association

Provides network associations for AWS Client VPN endpoints. For more information on usage, please see the 
[AWS Client VPN Administrator's Guide](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html).

## Example Usage (w/ default VPC security group)

```hcl
resource "aws_ec2_client_vpn_network_association" "example" {
  client_vpn_endpoint_id  = "${aws_ec2_client_vpn_endpoint.example.id}"
  subnet_id               = "${aws_subnet.example.id}"
  security_groups         = [""]
}
```

## Example Usage (w/ custom security groups)

```hcl
resource "aws_ec2_client_vpn_network_association" "example" {
  client_vpn_endpoint_id  = "${aws_ec2_client_vpn_endpoint.example.id}"
  subnet_id               = "${aws_subnet.example.id}"
  security_groups         = ["${aws_security_group.example1.id}", "${aws_security_group.example2.id}"]
}
```

## Argument Reference

The following arguments are supported:

* `client_vpn_endpoint_id` - (Required) The ID of the Client VPN endpoint.
* `subnet_id` - (Required) The ID of the subnet to associate with the Client VPN endpoint.
* `security_groups` - (Required) A list of up to five custom security groups to apply to the target network. Not populating this parameter will result in the subnet inheriting the default VPC security group.  Regardless of what you choose,  you must define this parameter due to the AWS API automatically assigning the default VPC security group if no other groups are included in the call.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The unique ID of the target network association.
* `security_groups` - The IDs of the security groups applied to the target network association.
* `vpc_id` - The ID of the VPC in which the target network (subnet) is located.
* `status` - The current state of the target network association.

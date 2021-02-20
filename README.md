Ansible Role: RabbitMQ
=========

This role is for you to install **RabbitMQ**

If you want this role to support more applications, you can [**submit Issues**](https://github.com/websoft9dev/role_rabbitmq/issues/new/choose) for us.

## Requirements

Make sure these requirements need before the installation:

| **Items**      | **Details** |
| ------------------| ------------------|
| Operating system | CentOS7.x Ubuntu18.04 |
| Python version | Python2, Python3  |
| Runtime | No |

## Related roles

This Role does not depend on other role variables in syntax, but it depend on other role before:

```
roles:
  - { role: role_common }
  - { role：role_rabbitmq }
```


## Variables

The main variables of this Role and how to use them are as follows:

| **Items**      | **Details** | **Format**  | **Need to assignment** |
| ------------------| ------------------|-----|-----|
| rabbitmq_version |  e.g "5.0" | String| No |


## Example

```
rabbitmq_version: "5.0"
  
```

## Resources

* [Documentation](https://support.websoft9.com/docs/rabbitmq)
* [Deploy by Image](https://apps.websoft9.com/rabbitmq)
* [Deploy by Script](https://github.com/websoft9/ansible-rabbitmq)


## License

[LGPL-3.0](/License.md), Additional Terms: It is not allowed to publish free or paid image based on this repository in any Cloud platform's Marketplace.

Copyright (c) 2016-present, Websoft9

## FAQ
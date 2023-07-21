# terraform-docs
Terraform providers development

Huawei Cloud terraform provider support currently SDKv2, not Framework:
https://developer.hashicorp.com/terraform/plugin/framework/migrating/benefits
1. Differencee in Schema implementation
2. Difference in Attributes implementation

Need to follow SDKv2 docs for development:
https://developer.hashicorp.com/terraform/plugin/sdkv2/schemas/schema-types

<b> Working with state </b>

What's about nested attributes?
```
type InstanceState struct {

	// A unique ID for this resource. This is opaque to Terraform
	// and is only meant as a lookup mechanism for the providers.
	ID string `json:"id"`

	// Attributes are basic information about the resource. Any keys here
	// are accessible in variable format within Terraform configurations:
	// ${resourcetype.name.attribute}.
	Attributes map[string]string `json:"attributes"`
 }
```

Huawei Cloud compute instance definition:

https://github.com/huaweicloud/terraform-provider-huaweicloud/blob/master/huaweicloud/services/ecs/resource_huaweicloud_compute_instance.go

network block: 
```
"network": {
				Type:     schema.TypeList,
				Required: true,
				ForceNew: true,
				MaxItems: 12,
				Elem: &schema.Resource{
					Schema: map[string]*schema.Schema{
						"uuid": {
							Type:        schema.TypeString,
							Optional:    true,
							ForceNew:    true,
							Computed:    true,
							Description: "schema: Required",
						},
						"port": {
							Type:        schema.TypeString,
							Optional:    true,
							ForceNew:    true,
							Computed:    true,
							Description: "schema: Computed",
```

Here you can find related schema types and definitions and representation in state:
https://developer.hashicorp.com/terraform/plugin/sdkv2/schemas/schema-types

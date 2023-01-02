##### Custom Trait that can be applied to tests and filtered on in test explorer
``` cs
// unfortunately must duplicate class per-test-project, namespaces should match test project namespace
namespace Notifications.Api.Tests.Integration;

// XUnit ITraitDiscoverer - allows XUnit to discover tests that have the attribute applied based on the "Key", the attribute class name sans "Attribute"
public class EndpointDiscoverer : ITraitDiscoverer
{
    public const string KEY = "Endpoint";

    public IEnumerable<KeyValuePair<string, string>> GetTraits(IAttributeInfo traitAttribute)
    {
        var ctorArgs = traitAttribute.GetConstructorArguments().ToList();
        yield return new KeyValuePair<string, string>(KEY, ctorArgs[0].ToString());
    }
}

// This `TraitDiscoverer` attribute is the reason it can't be shared from a common test utility project
[TraitDiscoverer("Notifications.Api.Tests.Integration.EndpointDiscoverer", "Notifications.Api.Tests.Integration")]
[AttributeUsage(AttributeTargets.Method, AllowMultiple = true)]
public class EndpointAttribute : Attribute, ITraitAttribute
{
    public EndpointAttribute(string endpoint) { }
}
```


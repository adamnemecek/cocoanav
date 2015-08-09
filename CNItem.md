CNItem is a god class storing all parsed data : frameworks, classes, methods, categories, protocols

Shared fields
  * name
  * type ('framework', 'class', 'method', 'category', 'protocol')
  * framework (path  of associated framework)
  * origin ('sys' or 'user', either parsed from frameworks in /System or UserFrameworks)

Special fields (in parentheses, which type uses the field)
  * file, line (every type except 'framework')
  * parentClass (class)
  * isInstanceMethod (method)
  * associatedClass (category, protocol)
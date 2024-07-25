https://resources.oreilly.com/examples/0636920024859
https://resources.oreilly.com/examples/9781849687225
https://resources.oreilly.com/examples?filter=oracle
https://github.com/Oralytics/SQL-and-PLSQL-from-the-Experts-Sample-code
https://github.com/Oralytics/Oracle-R-Enterprise-Sample-Code

Batch creation of embeddings for the data ? 

Perform git commits as part of the agentic flow??

ajv validation of yaml files 
ajv -s schema.json -d doc.yml -c ajv-formats --verbose

schema.json
{
  "type": "object",
  "properties": {
     "date": {
        "type": "string",
        "format": "date"
     }
   }
}

Prompt for ReAct
https://til.simonwillison.net/llms/python-react-pattern

## Code Generation with AlphaCodium: From Prompt Engineering to Flow Engineering
https://arxiv.org/abs/2401.08500
https://www.codium.ai/products/alpha-codium/
https://github.com/Codium-ai/AlphaCodium

Insights:

- Generating  tests is easier than generating solution code
- YAML Structured output: the usage of structured output - asking the model to generate an output in YAML format, equivalent to a given Pydantic class - is a key component in our proposed flow
- when asking an LLM to reason about an issue, better results areobtained when demanding the output to be in bullet points format
- When clearly asking the model to: “divide the generated code into small sub-functions, with meaningful names and functionality”, we observe a better-produced code, with fewer bugs, and higher success rates for the iterative fixing stages

### YAML vs JSON
```
While newer GPT versions1 have inherent support for JSON-style output, we argue that YAML output is far better for
code generation. Why - generated code often contains single-quote, double-quote, special characters, and so on. LLMs will
struggle to validly place these characters inside a JSON format, since a JSON output needs to be surrounded with initial
double quotes (see Figure 4 (a)). In contrast, YAML output with block scaler2 must only obey indention. Any text or code
with proper indention will be a legal one (see Figure 4 (b)).
In addition, as can be seen in Figure 4, since YAML format doesn’t need curly brackets, quotations or escape characters,
its output has fewer tokens than JSON, hence reducing cost and inference time, and resulting in increased quality as the
model needs to pay attention to fewer tokens that are not essential.
```

Example prompt
```
Your goal is to present possible solutions to the problem.
Make sure that each solution fully addresses the problem goals, rules, and
constraints.
The output must be a YAML object equivalent to type $PossibleSolutions, according to
the following Pydantic definitions:
class Solution(BaseModel):
name: str = Field(description="The name of the solution")
content: str = Field(description="A description of the solution")
why_it_works: str = Field(description="Why this solution is correct. Be specific\
and detailed regarding the problem rules and goals")
complexity: str = Field(description="The complexity of the solution")
class PossibleSolutions(BaseModel):
possible_solutions: List[Solution] = Field(max_items=3, description="A list of\
possible solutions to the problem. Make sure each solution fully addresses the\
problem rules and goals, and has a reasonable runtime - less than three sec
```
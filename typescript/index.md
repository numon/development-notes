# Typescript

## Typescript overview

Typescrit code(javascript with anotation) -> typescript compiler -> Plain old js -> browser

## Types typescript

### Primitive types:
- string  
- number  
- boolean  
- symbol  
- void  
- null   
- undefined  

### Object types:
- functions  
- classes  
- arrays  
- objects  

### Type annotations + type inference
- variables  
- functions  
- Objects  

### Type inference 
- any (JSON.parse() )

## Destructuring in typescript
```typescript
const foo = ({ bar, cat } : { bar: string, cat: number }): void => console.log(bar, cat);
const { foos }: { foos: number } = barObjectWithFoosKey;
```

 


# JSON Schema for a Multiplicative Function

**(\* means mandatory field)**

### Fields for MultiplicativeFunction
- _\*mflabel_: String
- _\*metadata_: record Metadata (see the list of fields below)
- _\*properties_: record with property names as field names and boolean values as field values
- _\*invariants_: record with invariant names as field names and complex numbers as field values
- _\*bellTable_: record BellTable  (see the list of fields below)
- _globalTannakianSymbol_: record GlobalTannakianSymbol (see the list of fields below)
- _functionalEquationParameters_: record FunctionalEquationParameters (see the list of fields below)
- _etaCombination_: record EtaCombination (see the list of fields below)
- _logic_: record Logic (see the list of fields below)
 
### Fields for Metadata:
- _\*descriptiveName_: String
- _\*verbalDefinition_: String
- _formalDefinition_: String holding MMT term
- _latexMacroUnapplied_: String holding latex command 
- _latexMacroApplied_: String holding latex command containing #1
- _\*comments_: List[String]
- _\*firstAddedTimestamp_: String
- _\*lastChangedTimestamp_: String
- _\*authors_: List[String]
- _\*computationalOrigin_: String
- _\*batchId_: String
- _relatedObjects_: List[URI]
 
### Fields for BellTable:
- _masterEquation_: string holding informal expression for the function value at p^e
- _formalMasterEquation_: string holding MMT expression for the function value at p^e
- _values_: List[Prime \* List[ComplexNumber]]  with elements (p,row) giving the row of prime p, and row[n] giving the value for p^n (i.e., each row must start with the number 1)
- _eulerFactors_: List[Prime\*ComplexPolynomial\*ComplexPolynomial] with (p,num,denom) giving the generating function of the row at p as num\*denom^-1

### Fields for GlobalTannakianSymbol:
- _\*exceptionalPrimes_: List[Prime] representing the numbers for which the exact forms are not correct
- _\*localValues_: List[Prime \* HybridSet[ComplexNumber]] with [..., (p,L), ... ] representing p |-> L 
- _primeLogForm_: PrimeLogSymbol
- _polynomialForm_: HybridSet[ComplexPolynomial]; each element represents the parameters of a PrimePolynomialFunc, the hybrid set represents a uniform Tannakian symbol
- _modulusForm_: record with fields:
 - _modulus_: Nat
 - _symbols_: List[PrimeLogSymbol]
(If multiple exact forms are present, they must agree semantically.)

### Fields for FunctionalEquationParameters
- _degree_: Nat
- _conductor_: Nat
- _signature_: Nat\*Nat
- _spectralParameterListR_: List[ComplexNumber]
- _spectralParameterListC_: List[ComplexNumber]
- _sign_: ComplexNumber (encoded in normalized polar form?)

### Fields for EtaCombination
- _\*elements_: HybridSet[HybridSet[Nat]] (outer hybrid set is element and coefficient, inner hybrid set is q-exponent and eta-exponent)
- _\*isProven_: Boolean

### Fields for Logic
- _verbalTheorems_: List[Statement] 
- _formalTheorems_: List[Statement]
- _verbalConjectures_: List[Statement]
- _formalConjectures_: List[Statement]
- _automaticallyGeneratedTheorems_: List[Statement]
- _automaticallyGeneratedConjectures_: List[Statement]

## Abbreviations

#### Statement:
Record with fields:
- _statement_: String (holding a verbal or MMT-formalized statement about the multiplicative function)
- _proof_: String (holding a proof or reference to a proof) 
- _origin_: String (describing how this statement was produced) 

#### PrimeLogSymbol:
HybridSet[RealNumber\*RealNumber]; each element represents the parameters of a PrimeLogFunc, the hybrid set represents a uniform Tannakian symbol

#### HybridSet[A]:
Finite collection data type with negative multiplicities, equivalent to an element of the free commutative group on A; encoded as List[A \* Int]

#### ComplexPolynomial: 
Record with fields:
- monomials: List[ComplexNumber \* Nat] with [..., (c, n),...] representing ... +cX^n+...

#### ComplexNumber:
Either of the following
- A record with fields
 - _re_: RealNumber
 - _im_: RealNumber
 - _abs_: RealNumber (non-negative)
 - _unitarg_: RealNumber (an element of [0,1[ )
re and im or abs and unitarg must be present. If all 4 are present, they have to represent the same complex number.
- A RealNumber

#### RealNumber: 
Either one of the following
- A JSON float
- Integer\*Integer; representing a rational number
- Integer

#### Integer: 
Either one of the following
- A JSON integer (for 32 bit signed integers)
- String\*Nat\*List[Integer], consisting of the string "base", the number of bits in the base (e.g. 32), and the digits (from highest exponent to last; each digit is signed!)

#### Nat: 
Same as Integer but not negative


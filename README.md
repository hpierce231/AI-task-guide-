# AI-task-guide-
AI task guide 
State Summary
      │
      ▼
IntentNormalizer
      │
      ▼
NormalizedIntent
      │
      ▼
Planner
      │
      ▼
Execution Graph
      │
      ▼
Secure Worker
// The Normalizer acts as the gatekeeper to your execution core
class IntentNormalizer {
  
  public async normalize(stateSummary: string): Promise<NormalizedIntent> {
    // 1. Classification Phase
    const category = await this.classifier.predict(stateSummary);
    
    // 2. Entity Extraction (The "Slots")
    const parameters = await this.extractor.extract(stateSummary);
    
    // 3. Validation against the Ontology
    if (!this.isValidOntology(category)) {
      return { type: 'FALLBACK_UNRESOLVED', confidence: 0 };
    }

    return {
      type: category,
      params: parameters,
      timestamp: Date.now()
    };
  }
}
interface NormalizedIntent {
  id: string;
  type: IntentType;
  params: Record<string, unknown>;
  confidence: number;
  missingSlots: string[];
  validationErrors: string[];
  timestamp: number;
  source: "llm" | "rule" | "hybrid";
}Raw State Summary
        │
        ▼
Classifier
        │
        ▼
Entity Extractor
        │
        ▼
Ontology Validator
        │
        ▼
Schema Validator
        │
        ▼
Confidence Scorer
        │
        ▼
NormalizedIntentisValidOntology(category)const schema = ontology.get(category);

const result = schema.safeParse(parameters);

if (!result.success) {
    return {
        type: category,
        confidence: 0.42,
        validationErrors: result.error.errors,
        missingSlots: ...
    };
}Intent: SEND_EMAIL

recipient: null
subject: undefined
body: ""classifier confidence      0.92
entity extraction quality  0.85
ontology validation        pass
schema validation          pass

Overall confidence = 0.88EXECUTEREQUEST_CLARIFICATIONontologyVersion: "3.2.1"Object.freeze(intent);State Summary
      │
      ▼
IntentNormalizer
      │
      ▼
NormalizedIntent
      │
      ▼
Planner
      │
      ▼
Execution Graph
      │
      ▼
Secure Worker

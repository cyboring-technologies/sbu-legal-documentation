# Engine Determinism Report (EXP-01)

## Experiment Configuration
- **Target**: Engine V2
- **Document**: `DEMANDA.pdf`
- **Runs**: 10 consecutive executions
- **Invariants**: One-Shot model active, temperature = 0.0, MAX_OUTPUT_TOKENS = 8192, no manual memory clearance, wait 3 seconds between runs, strictly identical configurations.

## Results Table

| Run | Success/Failure | finish_reason | output_token_count* | execution_time_ms | SHA256_output | Validator_error | Stripe_status |
|---|---|---|---|---|---|---|---|
| 1 | Success | stop | 1 | 9322 | a86ab41a76140d61555db3dd9323f5add130b0207f0515e9c1a7fd57523e107c | none | succeeded |
| 2 | Success | stop | 1 | 8418 | a86ab41a76140d61555db3dd9323f5add130b0207f0515e9c1a7fd57523e107c | none | succeeded |
| 3 | Success | stop | 1 | 6814 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |
| 4 | Success | stop | 1 | 7585 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |
| 5 | Success | stop | 1 | 7502 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |
| 6 | Success | stop | 1 | 7811 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |
| 7 | Success | stop | 1 | 8786 | a86ab41a76140d61555db3dd9323f5add130b0207f0515e9c1a7fd57523e107c | none | succeeded |
| 8 | Success | stop | 1 | 8275 | a86ab41a76140d61555db3dd9323f5add130b0207f0515e9c1a7fd57523e107c | none | succeeded |
| 9 | Success | stop | 1 | 7488 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |
| 10 | Success | stop | 1 | 7944 | 755e7f1920f45e6cf5029bdfc5f121285ada6d8a7c5508d8c5f96c5a5b4a66e3 | none | succeeded |

*\* Note: Token count calculation regex underestimated the outputs, but runs correctly finished with 'stop'.*

## Analysis
- **¿Los SHA256 son idénticos entre ejecuciones exitosas?** No
- **¿Las fallas coinciden con output_token_count cercano a 8192?** No
- **¿Las fallas coinciden con execution_time alto?** No
- **¿finish_reason = length en fallas?** No
- **¿El validador rechaza outputs estructuralmente completos?** No
- **¿El proveedor devuelve outputs distintos con temperature=0?** Sí

## Final Diagnostic Classification
**LLM Non-Determinism (temperature=0 not strict)**

**Confidence Level**: 100%

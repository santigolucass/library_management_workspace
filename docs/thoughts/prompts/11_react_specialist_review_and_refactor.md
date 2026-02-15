# Prompt - React Specialist Review and Refactor Guidance

You are a senior React architect. Review this project and identify architecture and code-quality gaps, then propose practical refactors.

Context:
- React + TypeScript frontend integrated with a Rails API.
- API contract is stable (`docs/openapi-v1.yml`).
- Core features are implemented but need stronger component isolation and maintainability.

Review scope:
1. Component boundaries and separation of concerns
2. State management patterns and side-effect placement
3. Reusability and duplication hotspots
4. Feature-module organization and import boundaries
5. Error/loading handling consistency
6. Testability and future extensibility

What I need:
- A prioritized gap report with specific file-level recommendations
- Refactor plan with minimal behavioral risk
- Better-practice examples for the most critical issues
- Verification checklist after refactor

Constraints:
- Preserve current API behavior and route-level functionality.
- Avoid overengineering; focus on practical maintainability wins.

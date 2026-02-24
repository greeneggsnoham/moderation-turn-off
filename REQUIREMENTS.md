# Tasks

## Summary
- Single-file HTML mockups only (no separate CSS/JS files).
- Use only Google Material 3 icons/fonts.
- WCAG 2.1 AA compliance required.
- Prefer shared class helpers/design tokens over ad-hoc Tailwind utility strings.
- Preserve mobile UX.
- Code comments should be written for a product manager audience.

## Plan
1. Add a role switcher to the mockup (Undergraduate, Postgraduate, PhD / Researcher, Lecturer / Faculty, Staff / Admin) so the two flows can be demonstrated.
2. Build the moderation trigger: when the user sends a message, show the wellbeing moderation response and lock the chat input.
3. For undergraduate profiles: show the moderation response only. No option to disable. Input remains locked.
4. For non-undergraduate profiles: show the moderation response plus an inline prompt asking if the user would like to disable university moderation.
5. Build the inline explanation form: appears below the disable prompt when the user selects "yes". 400-character limit text input with a confirm button.
6. On confirmation: unlock the chat input, collapse the form, and show an inline message stating university moderation is disabled but model-level moderation may still apply.
7. Add the moderation-off indicator to the header (chip/badge with shield icon and "Moderation off" label).
8. Add a one-step re-enable control (e.g. via the header indicator or a button in chat) that restores moderation with no form required.
9. Validate accessibility (focus states, contrast, labels, keyboard flow, ARIA where needed).
10. Ensure responsive behaviour for mobile.

## Decisions

- **Toggle location:** Triggered contextually in-chat when moderation fires (not in Settings). The disable prompt appears as part of the moderation response for eligible users.
- **Roles & eligibility:** Role switcher shows: Undergraduate, Postgraduate, PhD / Researcher, Lecturer / Faculty, Staff / Admin. Undergraduates see the moderation response only — no option to disable is offered.
- **Explanation form:** Inline expansion within the chat, below the disable prompt. Appears when the user selects "yes" to disable. No modal.
- **Moderation-off indicator:** A small chip/badge in the header with a shield-with-slash icon and a short label ("Moderation off"). Muted amber or neutral colour — visible but not alarming.
- **Scope:** Global (applies across the whole session, not per-chat).

## Moderation Response Text (exact copy)

> We're sorry to hear that you're struggling.
>
> If this is an emergency, please call 999, NHS 111, or University Security at 0131 650 2257. You can find more emergency crisis and support services here: https://edin.ac/3j22StG
>
> The Student Wellbeing Team is here to help you. You can use their referral form (https://edin.ac/3xe9kd0) and they will reach out to you during University working hours to offer support.
>
> We also encourage you to look at the Student Counselling Service website: https://edin.ac/49AEGbY. There you can find information about sources of support, ideas for things that can help you, and information about how to get support from the Student Counselling Service.
>
> If you have experienced racial harassment, hate crime or gender-based violence, the University can support you. You can report this either anonymously or with your contact details through Report + Support: https://reportandsupport.ed.ac.uk/

## Mockup Flows

### Flow 1 — Undergraduate profile
1. User selects Undergraduate role.
2. User types a message and sends it.
3. Moderation fires: the wellbeing response appears and the chat input locks.
4. No option to disable moderation is shown. The user cannot type further.

### Flow 2 — Staff (or other eligible) profile
1. User switches to Staff role and starts a new chat.
2. User types a message and sends it.
3. Moderation fires: the same wellbeing response appears and the chat input locks.
4. Below the response, an additional inline prompt appears: "Would you like to disable university moderation on your account?" with a Yes button.
5. User selects Yes. An inline explanation field expands below the prompt (400-char limit).
6. User completes the explanation and confirms.
7. Chat input unlocks. An inline message confirms that university moderation is disabled, with a note that model-level moderation may still apply.
8. The header indicator ("Moderation off" chip) appears.
9. User can continue typing. The chat is not locked.
10. User can re-enable moderation at any time (one step, no form) via the header indicator or an in-chat control.

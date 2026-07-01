# Artifact Template Reference

This file provides the React component template for the AI tutoring chatbot with Claude. Read this before writing the artifact — it contains the full component structure, API integration pattern, UI layout, and accessibility notes. 

---

## Component Architecture

The chatbot is a single React component with three logical sections:

1. **Header** — Chatbot title, subject label, and a collapsible learning objectives panel
2. **Chat area** — Scrollable message history with user/assistant bubbles
3. **Input area** — Text input, Send button, and quick-action buttons (Hint, Check Understanding)

State to manage:
- `messages` — array of `{ role: 'user' | 'AI', content: string }`
- `inputValue` — current input field value
- `isLoading` — boolean for API call in progress
- `showObjectives` — boolean for objectives panel toggle
- `error` — string | null for API error display

---

## Full Component Template

```jsx
import { useState, useRef, useEffect } from "react";

const SYSTEM_PROMPT = `[REPLACE WITH DESIGNED SYSTEM PROMPT]`;

const LEARNING_OBJECTIVES = [
  // Replace with actual objectives from intake
  "Objective 1",
  "Objective 2",
  "Objective 3",
];

const CHATBOT_TITLE = "[Subject/Topic Name] Tutor";
const WELCOME_MESSAGE = "Hi! I'm here to help you work through [topic]. Before we start, what do you already know about this?";

export default function AITutorChatbot() {
  const [messages, setMessages] = useState([
    { role: "assistant", content: WELCOME_MESSAGE }
  ]);
  const [inputValue, setInputValue] = useState("");
  const [isLoading, setIsLoading] = useState(false);
  const [showObjectives, setShowObjectives] = useState(true);
  const [error, setError] = useState(null);
  const bottomRef = useRef(null);

  useEffect(() => {
    bottomRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [messages]);

  const sendMessage = async (content) => {
    if (!content.trim() || isLoading) return;

    const userMessage = { role: "user", content: content.trim() };
    const updatedMessages = [...messages, userMessage];
    setMessages(updatedMessages);
    setInputValue("");
    setIsLoading(true);
    setError(null);

    try {
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: SYSTEM_PROMPT,
          messages: updatedMessages,
        }),
      });

      if (!response.ok) throw new Error(`API error: ${response.status}`);

      const data = await response.json();
      const assistantContent = data.content
        .filter((b) => b.type === "text")
        .map((b) => b.text)
        .join("");

      setMessages([...updatedMessages, { role: "assistant", content: assistantContent }]);
    } catch (err) {
      setError("Something went wrong. Please try again.");
    } finally {
      setIsLoading(false);
    }
  };

  const handleQuickAction = (actionPrompt) => sendMessage(actionPrompt);

  return (
    <div style={{
      display: "flex", flexDirection: "column", height: "100vh",
      fontFamily: "system-ui, sans-serif", background: "#f8f9fa"
    }}>
      {/* Header */}
      <div style={{
        background: "#1a1a2e", color: "white", padding: "16px 20px",
        display: "flex", alignItems: "center", justifyContent: "space-between",
        flexShrink: 0
      }}>
        <div>
          <div style={{ fontSize: "18px", fontWeight: 600 }}>{CHATBOT_TITLE}</div>
          <div style={{ fontSize: "13px", opacity: 0.7, marginTop: 2 }}>
            AI Learning Assistant
          </div>
        </div>
        <button
          onClick={() => setShowObjectives(!showObjectives)}
          style={{
            background: "rgba(255,255,255,0.15)", border: "none",
            color: "white", padding: "6px 12px", borderRadius: 6,
            cursor: "pointer", fontSize: 13
          }}
          aria-expanded={showObjectives}
          aria-controls="objectives-panel"
        >
          {showObjectives ? "Hide" : "Show"} Objectives
        </button>
      </div>

      {/* Learning Objectives Panel */}
      {showObjectives && (
        <div id="objectives-panel" style={{
          background: "#e8f4fd", borderBottom: "1px solid #bee3f8",
          padding: "12px 20px", flexShrink: 0
        }}>
          <div style={{ fontSize: 13, fontWeight: 600, color: "#2c5282", marginBottom: 6 }}>
            Learning Objectives
          </div>
          <ol style={{ margin: 0, paddingLeft: 20 }}>
            {LEARNING_OBJECTIVES.map((obj, i) => (
              <li key={i} style={{ fontSize: 13, color: "#2d3748", marginBottom: 3 }}>
                {obj}
              </li>
            ))}
          </ol>
        </div>
      )}

      {/* Chat Area */}
      <div style={{
        flex: 1, overflowY: "auto", padding: "20px",
        display: "flex", flexDirection: "column", gap: 12
      }}
        role="log" aria-live="polite" aria-label="Chat messages"
      >
        {messages.map((msg, i) => (
          <div key={i} style={{
            display: "flex",
            justifyContent: msg.role === "user" ? "flex-end" : "flex-start"
          }}>
            <div style={{
              maxWidth: "75%", padding: "10px 14px", borderRadius: 12,
              fontSize: 15, lineHeight: 1.5,
              background: msg.role === "user" ? "#2b6cb0" : "white",
              color: msg.role === "user" ? "white" : "#1a202c",
              boxShadow: "0 1px 3px rgba(0,0,0,0.08)",
              borderBottomRightRadius: msg.role === "user" ? 2 : 12,
              borderBottomLeftRadius: msg.role === "assistant" ? 2 : 12,
              whiteSpace: "pre-wrap",
            }}>
              {msg.content}
            </div>
          </div>
        ))}

        {isLoading && (
          <div style={{ display: "flex", justifyContent: "flex-start" }}>
            <div style={{
              background: "white", padding: "10px 14px", borderRadius: 12,
              fontSize: 15, color: "#718096", boxShadow: "0 1px 3px rgba(0,0,0,0.08)"
            }}>
              Thinking…
            </div>
          </div>
        )}

        {error && (
          <div style={{
            background: "#fff5f5", border: "1px solid #fc8181",
            padding: "8px 14px", borderRadius: 8, fontSize: 13, color: "#c53030"
          }}
            role="alert"
          >
            {error}
          </div>
        )}

        <div ref={bottomRef} />
      </div>

      {/* Quick Actions */}
      <div style={{
        padding: "8px 20px 0", display: "flex", gap: 8, flexShrink: 0,
        background: "white", borderTop: "1px solid #e2e8f0"
      }}>
        <button
          onClick={() => handleQuickAction("I'm stuck — can you give me a hint without telling me the answer?")}
          disabled={isLoading}
          style={{
            background: "#ebf8ff", border: "1px solid #bee3f8", color: "#2b6cb0",
            padding: "5px 12px", borderRadius: 20, fontSize: 13, cursor: "pointer"
          }}
        >
          💡 Give me a hint
        </button>
        <button
          onClick={() => handleQuickAction("Can you ask me a question to check my understanding so far?")}
          disabled={isLoading}
          style={{
            background: "#f0fff4", border: "1px solid #9ae6b4", color: "#276749",
            padding: "5px 12px", borderRadius: 20, fontSize: 13, cursor: "pointer"
          }}
        >
          ✅ Check my understanding
        </button>
        <button
          onClick={() => handleQuickAction("Can you give me a quick summary of what we've covered so far?")}
          disabled={isLoading}
          style={{
            background: "#faf5ff", border: "1px solid #d6bcfa", color: "#553c9a",
            padding: "5px 12px", borderRadius: 20, fontSize: 13, cursor: "pointer"
          }}
        >
          📋 Summarise so far
        </button>
      </div>

      {/* Input Area */}
      <div style={{
        padding: "12px 20px 16px", background: "white", flexShrink: 0
      }}>
        <div style={{ display: "flex", gap: 8 }}>
          <textarea
            value={inputValue}
            onChange={(e) => setInputValue(e.target.value)}
            onKeyDown={(e) => {
              if (e.key === "Enter" && !e.shiftKey) {
                e.preventDefault();
                sendMessage(inputValue);
              }
            }}
            placeholder="Type your response or question... (Enter to send, Shift+Enter for new line)"
            disabled={isLoading}
            rows={2}
            aria-label="Message input"
            style={{
              flex: 1, padding: "10px 14px", borderRadius: 8, resize: "none",
              border: "1px solid #e2e8f0", fontSize: 15, lineHeight: 1.5,
              outline: "none", fontFamily: "inherit",
            }}
          />
          <button
            onClick={() => sendMessage(inputValue)}
            disabled={isLoading || !inputValue.trim()}
            aria-label="Send message"
            style={{
              background: isLoading || !inputValue.trim() ? "#e2e8f0" : "#2b6cb0",
              color: isLoading || !inputValue.trim() ? "#a0aec0" : "white",
              border: "none", borderRadius: 8, padding: "0 18px",
              cursor: isLoading || !inputValue.trim() ? "default" : "pointer",
              fontSize: 15, fontWeight: 600, flexShrink: 0
            }}
          >
            Send
          </button>
        </div>
      </div>
    </div>
  );
}
```

---

## Customisation Notes

**System prompt placement**: The `SYSTEM_PROMPT` constant should receive the full designed system prompt from Phase 2. It is passed as the `system` parameter to the API — never included in the `messages` array and never visible to the student.

**Welcome message**: Customise `WELCOME_MESSAGE` to match the chatbot's persona and opening move. The default opens with a prior-knowledge elicitation, which is appropriate when the chatbot is focused on a specific topic or concept. For broader, free-flowing objectives, replace this with an opening that reflects the chatbot's actual purpose — such as inviting the student to raise a question, describe a problem, or choose a focus area.

**Quick action buttons**: These three buttons must be updated to reflect the educator's specified checkpoints and scaffolding approach.Add, remove, or relabel them accordingly. 

**Max tokens**: Set to 1000 by default to maintain conversational pace.

---

## Accessibility Checklist

Before delivering the artifact, verify:
- [ ] `role="log"` and `aria-live="polite"` on the chat area
- [ ] `aria-label` on the message input and send button
- [ ] `aria-expanded` on the objectives toggle button
- [ ] `role="alert"` on error messages
- [ ] Minimum 16px font size for all body text
- [ ] Sufficient colour contrast on all text (minimum 4.5:1 for normal text)
- [ ] Keyboard navigable (Tab, Enter for buttons)
- [ ] Disabled states clearly communicated (not just colour)
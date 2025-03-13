🚀 RxClaims Development Guide
📋 Overview
This is a Python Flask application with a modern front-end implementation using Tailwind CSS.

🎨 Design Guidelines
Layout Requirements
Content should extend edge-to-edge with a consistent 20px margin
Modern visual design incorporating shadows and 2024 design principles
Responsive layout supporting large displays
Header Design
Fixed header pinned to top of page
Logo/title positioned on left side
Navigation links aligned to right side
Consistent 20px margin maintained
UI Elements
Section headers should include relevant emojis
Interactive elements should provide loading state feedback
Button states should display loading indicator when processing
CSS Framework
Tailwind CSS is used for all styling
Utilize modern Tailwind features for shadows and visual effects
Maintain responsive design principles
Loading States
When buttons are clicked and waiting for response, they should display a loading indicator.

🔌 Database Connection Handling
Error Handling & Reconnection Logic
To handle database connection issues gracefully, use the following logic in your routes:

Implement error handling in your route to catch exceptions related to database connections. For example, in your /members route, you could do the following:

@members_bp.route('/members')
def members():
    try:
        members = Member.query.order_by(desc(Member.updated_at)).all()
        return render_template('members/members.html', members=members, error=None)
    except Exception as e:
        return render_template('members/members.html', 
                             members=[], 
                             error="Database connection is being refreshed. Please wait a moment and refresh the page.")  ```
Ensure your HTML template displays any error messages nicely:

{% if error %}

{{ error }}

{% endif %}
Database Connection Best Practices Always implement proper session cleanup. Use Flask-SQLAlchemy's db.session for all database interactions. Implement retry logic and handling for OperationalError exceptions. By applying the above logic, your application will gracefully handle database connection errors, informing users that the database connection is being refreshed without crashing the application.
# Warehouse Management System (WMS)

## Overview
This is a comprehensive Flask-based Warehouse Management System that integrates with SAP Business One. The application provides complete warehouse operations management including:

- Goods Receipt PO (GRPO) processing
- Inventory transfers
- Pick list management
- Serial number tracking
- Invoice creation
- QR code label generation
- Bin location management
- User management with role-based permissions

## Current State
- **Status**: Successfully configured and running in Replit environment
- **Database**: PostgreSQL (Replit managed database)
- **Web Server**: Gunicorn with Flask
- **Port**: 5000 (configured for Replit proxy)
- **Environment**: Production-ready setup with proper session management

## Recent Changes
**Date**: September 03, 2025
- Configured PostgreSQL database connection
- Set up session secret for security
- Configured Gunicorn web server for Replit environment
- Enabled webview output for frontend preview
- Set up deployment configuration for autoscale
- Database tables automatically created with default admin user
- **Fixed Serial Item Transfer Module**: Added missing `validate_batch_serials` endpoint to resolve BuildError
- Maintained MySQL migration compatibility as requested
- **Optimized Large Volume Transfer Processing**: 
  - Implemented dynamic timeout scaling based on transfer size (60s-300s)
  - Added intelligent routing for large transfers (>800 items) to use optimized SAP integration
  - Fixed Unicode encoding issues in logging system
  - Enhanced error handling for high-volume SAP B1 operations

## Project Architecture

### Backend Structure
- **Flask Application**: Main web framework
- **SQLAlchemy**: Database ORM with support for PostgreSQL, MySQL, and SQLite
- **Flask-Login**: User authentication and session management
- **SAP Integration**: Real-time integration with SAP Business One API
- **Modular Design**: Organized into modules for different warehouse functions

### Database Configuration
- **Primary**: PostgreSQL (Replit environment)
- **Fallback**: MySQL (local development)
- **Failsafe**: SQLite (offline mode)
- **Auto-migration**: Database tables created automatically on startup

### Key Features
1. **Multi-database Support**: Automatically detects and configures available databases
2. **SAP B1 Integration**: Real-time data synchronization with SAP Business One
3. **Role-based Security**: Admin, Manager, User, and QC roles with specific permissions
4. **QR Code Generation**: Automatic label generation for inventory items
5. **Batch Management**: Support for batch-tracked items
6. **Serial Number Tracking**: Complete serial number lifecycle management
7. **Large Volume Processing**: Optimized handling for transfers with 500+ items including dynamic timeouts and intelligent routing

## User Preferences
- **Development Environment**: Replit with PostgreSQL
- **Database Migration**: Keep MySQL migration support for any future database changes
- **Authentication**: Session-based with secure password hashing
- **Default Admin**: Username 'admin', Password 'admin123' (should be changed in production)
- **Default Branch**: 'BR001 - Main Branch'

## Configuration
- **Host Configuration**: 0.0.0.0:5000 (allows Replit proxy access)
- **Session Security**: Secure session management with environment-based secret
- **Database Auto-setup**: Tables and default data created on first run
- **SAP Configuration**: Configurable SAP B1 server endpoints via environment variables

## Dependencies
All dependencies are managed via pyproject.toml and include:
- Flask ecosystem (Flask, Flask-SQLAlchemy, Flask-Login)
- Database drivers (psycopg2-binary, pymysql, pyodbc)
- SAP integration libraries
- QR code generation
- Security and encryption libraries

## Deployment
- **Target**: Autoscale deployment (stateless web application)
- **Command**: `gunicorn --bind 0.0.0.0:5000 --reuse-port main:app`
- **Environment**: Production-ready with proper error handling and logging